# FastAPI

Earlier editions of this handbook recommended Flask for building APIs in Python. That recommendation is now retired. **Use FastAPI.**

## Why FastAPI over Flask

Flask was a great choice for a long time. The ecosystem moved on. FastAPI is what most new Python APIs are built with, and for good reasons:

- **Automatic interactive docs.** FastAPI generates an OpenAPI spec from your code, and serves a live interactive documentation UI at `/docs`. This is genuinely transformative for clinical APIs, where the documentation is also the contract.
- **Type hints all the way.** Request and response models are defined as Pydantic classes. The same code that defines the model also validates the input, serialises the output, and generates the schema.
- **Async first.** FastAPI is built on `async`/`await`. For I/O-bound clinical work (database calls, FHIR API calls, terminology lookups), async lets a single process handle far more concurrent requests.
- **Speed.** FastAPI is one of the fastest Python frameworks. Not as fast as Rust, but more than fast enough for anything an NHS clinical service needs.
- **Modern, well-documented, actively maintained.** The Flask momentum has slowed. FastAPI is where the community energy is.

## A minimal FastAPI app

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class CreatinineInput(BaseModel):
    sex: str
    serum_creatinine_umol_l: float
    age: int

class EgfrResult(BaseModel):
    egfr_ml_min_1_73m2: float
    formula: str = "CKD-EPI 2021"

@app.post("/egfr", response_model=EgfrResult)
def calculate_egfr(payload: CreatinineInput) -> EgfrResult:
    # placeholder calculation; do not use clinically
    egfr = 100.0
    return EgfrResult(egfr_ml_min_1_73m2=egfr)
```

Run it with `uvicorn main:app --reload`. Visit `http://localhost:8000/docs` and you have an interactive Swagger UI for free.

## Getting started

- Install: `pip install fastapi uvicorn[standard]`
- Recommended project layout: a `src/` package, an `app` module that creates the FastAPI instance, separate modules for routers (one per resource), Pydantic models in their own module.
- Use `uvicorn` for development and behind `gunicorn` (or directly behind a process manager) in production.
- Containerise with Docker for deployment. The official Python images plus uvicorn make for a small, fast image.

## FHIR endpoints with FastAPI

FastAPI plus the `fhir.resources` library is a particularly good combination. Both are Pydantic-native, so a FHIR Resource can be a request or response model directly. Example:

```python
from fastapi import FastAPI
from fhir.resources.patient import Patient

app = FastAPI()

@app.post("/Patient", response_model=Patient)
def create_patient(patient: Patient) -> Patient:
    # validate, persist, return
    return patient
```

The OpenAPI documentation generated from this code will reflect the full FHIR Patient schema. See [FHIR and Interoperability](../advanced/fhir-and-interoperability.md) for more.

## Authentication

FastAPI has good built-in support for OAuth2 password flow and JWT bearer tokens. For NHS-facing APIs, you'll typically integrate with NHS login or NHS CIS2 via OpenID Connect. There's no FastAPI-specific NHS library yet that I'd recommend without reservation; check the NHS England Developer Hub for the current state.

## Testing

FastAPI has first-class testing support via `TestClient` (built on `httpx`). Tests look like:

```python
from fastapi.testclient import TestClient
from .main import app

client = TestClient(app)

def test_egfr_calculation():
    response = client.post(
        "/egfr",
        json={"sex": "male", "serum_creatinine_umol_l": 88, "age": 50},
    )
    assert response.status_code == 200
    assert response.json()["formula"] == "CKD-EPI 2021"
```

For clinical APIs, write a test for every endpoint and every clinically-significant input range. See [Clinical Safety](../advanced/clinical-safety.md) for more on testing strategies.

## When to use Django instead

FastAPI is for APIs. If you also need a templated web frontend, an admin interface, ORM integration, user management, and auth all in one place, Django is the better choice. See [Web Frameworks](web-frameworks.md) and [Learning Django](learning-django.md).

A common pattern: Django for the full-stack web app, FastAPI for separate microservices that expose APIs. They coexist happily.
