# FHIR and Interoperability

If you build clinical software for any length of time, you will run into FHIR. Better to meet it on purpose than by surprise.

## What is FHIR and why should I care?

FHIR (Fast Healthcare Interoperability Resources, pronounced 'fire') is the modern standard for exchanging healthcare data. It's a REST-style API specification with a defined set of clinical 'Resources' (Patient, Observation, MedicationRequest, Encounter, and so on), each with a JSON or XML representation.

You should care because:

- It is the NHS's preferred interoperability standard for new work.
- The NHS England digital strategy mandates FHIR for new APIs.
- Most modern clinical APIs in the UK and internationally are FHIR-based.
- If you publish a clinical API and it isn't FHIR, you'll be asked why.

FHIR is not perfect. The specification is huge, the resources are deliberately broad, and 'we use FHIR' often means very different things in different organisations. But it has critical mass, which matters more than purity.

## FHIR R4 and R5

FHIR R4 (released 2019) is the workhorse version. It is the version mandated by NHS England for current work. Most NHS APIs are R4.

FHIR R5 (released 2023) is the latest normative release. Adoption is gradual. If you're starting now, build for R4 with an eye on R5.

There is also an emerging UK Core profile set, which constrains the broad FHIR spec to UK NHS use cases. If you're building for the NHS, look at UK Core profiles before defining your own.

## Practical FHIR

Some things to know before you start:

- **Read the spec.** Or at least skim it. <https://hl7.org/fhir/R4/> is the canonical reference.
- **Use a Python library.** The two main options are `fhir.resources` (Pydantic-based, type-safe) and `fhirclient` (older, less maintained). I use `fhir.resources`.
- **Use a public test server while learning.** HAPI FHIR runs a public R4 server at <https://hapi.fhir.org/baseR4>. You can POST resources, query them, and explore the API surface without setting anything up.
- **Validate your resources.** A resource that's structurally valid JSON but doesn't match the FHIR spec will be rejected by any real server. Validate locally before sending.

A minimal example of building a FHIR Patient in Python with `fhir.resources`:

```python
from fhir.resources.patient import Patient
from fhir.resources.humanname import HumanName

patient = Patient(
    name=[HumanName(family="Bloggs", given=["Joe"])],
    gender="male",
    birthDate="1980-01-01",
)
print(patient.json(indent=2))
```

For an API, see [FastAPI](../getting-started/fastapi.md). FastAPI plus `fhir.resources` is a productive stack for FHIR endpoints because both are Pydantic-native.

## SNOMED CT, LOINC, dm+d

FHIR resources reference clinical terminologies, but doesn't define them. The big three for UK practice are:

- **SNOMED CT.** The clinical terminology mandated for use in NHS records. Vast (over 350,000 active concepts), hierarchical, polyhierarchical, multilingual. The NHS has a UK Edition.
- **LOINC.** The terminology for laboratory and clinical observations. If you're representing a test result in FHIR, the test code is usually a LOINC code.
- **dm+d.** The Dictionary of Medicines and Devices. The UK's terminology for medications. If you're representing a prescription in FHIR for the NHS, dm+d is what you use.

Practical notes:

- The **NHS Terminology Server** (<https://ontology.nhs.uk/>) is the authoritative source for current UK SNOMED, dm+d, and other terminologies. It exposes a FHIR Terminology API.
- For local SNOMED work, a Python library like `pymedtermino` is one option. There are also several open SNOMED servers (Snowstorm is the reference implementation).
- **Don't roll your own.** Don't store your own copy of SNOMED in a CSV and expect it to stay current. Use a terminology service.

## Common pitfalls

- **'We use FHIR' is not interoperability.** Two systems can both speak FHIR and still not exchange data, because they use different profiles, different terminologies, or different reference patterns. Interoperability requires shared semantics, not just shared syntax.
- **Big-bang FHIR projects fail.** Start with one resource, one use case, one consumer. Get that right, then add the next.
- **Don't over-fit to one vendor's FHIR.** Major EHR vendors each have their own quirks. Build to the spec, not to one implementation.
- **Cardinality matters.** FHIR Resources allow many fields to be optional or repeating. Real consumers will rely on specific fields being present. Document what you populate.

## When NOT to use FHIR

FHIR is a wire format. It's not always the right internal model. For your application's internal data, you may want a simpler representation that you map to FHIR at the API boundary. Trying to use FHIR resources as your internal data model often produces awkward code.

If you're building something purely internal, with no interoperability requirement, you don't have to use FHIR. Use the simplest model that fits the problem. But if you are exposing data outside your application, FHIR is the default answer.

## Resources

- HL7 FHIR R4: <https://hl7.org/fhir/R4/>
- NHS England FHIR guidance: <https://digital.nhs.uk/developer/api-catalogue>
- NHS Terminology Server: <https://ontology.nhs.uk/>
- HAPI FHIR public test server: <https://hapi.fhir.org/baseR4>
- UK Core profiles: <https://simplifier.net/HL7FHIRUKCoreR4>
