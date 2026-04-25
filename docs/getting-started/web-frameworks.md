# Web Frameworks

Most of what a clinician-developer builds is, in some form, a web application. Either a server-rendered web app, or an API consumed by another application, or a single-page application backed by an API.

For each of these, the Python answer is opinionated.

## What is a Web Framework?

A web framework is a library that handles the boring, repetitive parts of building a web application: routing URLs to functions, parsing requests, generating responses, handling forms, talking to a database, managing user sessions. It lets you focus on the parts that are specific to your application.

Without a framework you can build a web application from scratch using lower-level tools (the standard library `http.server`, the `wsgiref` module, raw sockets). You almost never want to.

## The opinionated recommendations

- **Django** for full-stack web applications.
- **FastAPI** for APIs.
- That's it.

The previous edition of this handbook also recommended Flask. Flask is fine, and there's a lot of Flask code in the world that isn't going anywhere. But for new work, FastAPI is the better choice for APIs and Django is the better choice for full-stack web. There is no longer a strong argument for Flask in 2026.

## Django for full-stack

Use Django when you need:

- Server-rendered HTML pages.
- A database with an ORM.
- A built-in admin interface (this is genuinely a superpower for clinical projects: you get a usable data-management UI for free).
- User authentication, sessions, permissions.
- Forms, file uploads, email, internationalisation.
- Robustness and longevity (Django turns 20 next year and is still excellent).

Django is the answer for most clinical apps that have a UI. The admin interface alone justifies it for anything where clinicians need to view, search, or edit structured data without you having to build the UI from scratch.

For learning Django, see [Learning Django](learning-django.md).

## FastAPI for APIs

Use FastAPI when you need:

- A REST or REST-style API.
- Automatic interactive API documentation.
- Type-checked request and response models.
- Async support (for I/O-heavy work).
- Speed.

FastAPI is the modern Python answer for building APIs, particularly FHIR APIs (which Pydantic models map onto naturally). See [FastAPI](fastapi.md) and [FHIR and Interoperability](../advanced/fhir-and-interoperability.md).

## Combining Django and FastAPI

For non-trivial applications, you'll often want both:

- **Django** for the user-facing web app, the admin, the auth.
- **FastAPI** for separate API services that the Django app (and others) consume.

They run as separate processes and talk over HTTP. This is the same shape as 'monolith plus microservice' you'd see in any modern stack. For small teams, don't over-do it: one Django app does an enormous amount on its own. Reach for a separate FastAPI service when you have a real reason (a different scaling profile, a different deployment cadence, a need to expose the API to other consumers).

## What about frontend frameworks?

If your application needs a rich, interactive frontend (drag-and-drop, real-time updates, complex client-side state), you'll end up using a frontend framework: React, Vue, Svelte, or Solid.

A few points worth understanding before you reach for one:

- **You're now building two applications.** A frontend (running in the user's browser) and a backend (running on your server). This roughly doubles the work and the surface area for bugs.
- **Auth is harder.** Server-rendered apps get auth for almost free; SPAs need careful handling of tokens, refresh, and session lifecycle.
- **Server-rendered HTML is making a comeback.** Patterns like HTMX, Turbo, and Phoenix LiveView let you build interactive web apps without a full SPA. For most clinical CRUD applications, server-rendered HTML with judicious sprinkles of JavaScript (or HTMX) is enough and is a lot less work.
- **Developer time is more expensive than CPU cycles.** Whether those cycles are yours on a server or the user's in their browser. Don't pay the SPA tax unless your application genuinely needs it.

If you do reach for a frontend framework, **React** is the safe default for the same reasons VS Code is the safe default editor: largest community, best documentation, most hireable, most AI tools assume you're using it.

## Mobile apps

Three honest options:

- **Don't build one.** A responsive mobile-friendly web app is enough for most clinical use cases. You can add it to the home screen and it behaves like an app.
- **React Native** if you really do need a native app and you're already using React. One codebase for iOS and Android, performance is good for clinical apps.
- **Flutter** (Dart) if you want a more native-feeling cross-platform experience. It's what RCPCH uses for the digital growth charts app, for example. Steeper learning curve than React Native if you don't know Dart.

A native app is rarely worth it for a clinician-developer's first project. The distribution mechanics (Apple App Store, Google Play, organisational MDM) alone are a substantial undertaking.

!!! tip "Mantra: Clinicians are smart and can learn code if they want"
    A clinician of any kind, any level, and any background, is *by definition* intelligent and motivated and capable. That's **you**. You can learn to code just as you learned all the other things you needed to learn to develop your professional skills.
