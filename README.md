# Step-by-Step Introduction to the Vue.js Framework

📖 **Read the tutorial: [https://stahe.github.io/en-vuejs-etape-par-etape-sept-2026/](https://stahe.github.io/en-vuejs-etape-par-etape-sept-2026/)**

This course teaches you how to build a web application using the [Vue.js](https://vuejs.org) 3 framework: a **single-page application** (SPA), where pages are rendered **in the browser** using JSON data from a server.

It follows up on the course [Step-by-Step Introduction to the NestJS Web Framework](https://stahe.github.io/en-nestjs-html-sept-2026/), offering a different perspective:

| NestJS Course | Vue.js Course |
|---|---|
| the server renders HTML pages (Handlebars) | the browser renders pages (Vue.js) |
| the browser displays what it receives | the server returns only JSON |
| controllers, views, `res.render` | `.vue` components, router, stores |
| dictionaries read by the server | dictionaries on the client (vue-i18n); the server returns only keys |
| flash message in a cookie | flash message in a Pinia store |

The pages themselves remain unchanged: they are the same ones from the **RdvMedecins** application already presented with the other frameworks.

## The Approach: Many Short Examples, Then a Case Study

The course is structured around **20 short examples**, each focused on a single concept. They share a single `npm install` command and a single development server (Vite), which displays their table of contents.

| Chapter | Content | Examples |
|---|---|---|
| Getting Started | a Vite project, `ref` / `reactive` / `computed` / `watch`, directives, events, forms, validation | 01–06 |
| Components | props, events, `v-model` on a component, slots, lifecycle, composables, `provide` / `inject`, confirmation dialog | 07–12 |
| Routing | vue-router, parameters, query, navigation guards, lazy loading | 13–14 |
| Shared State | Pinia stores, `localStorage` | 15 |
| Internationalization | vue-i18n: settings, plurals, dates, numbers | 16 |
| The Server: A Black Box | Installing the JSON server, its API, 48 `curl` examples | – |
| Communicating with the server | `fetch`, Vite proxy, `httpOnly` cookie, API access layer, server errors | 17–20 |

Each example is presented with its complete code, commented line by line, and a screenshot of its execution.

## The server: a black box

The server is the NestJS server from the previous lesson, whose controllers now return **JSON**. This lesson treats it as a **black box**: we set it up, study its API, and query it with `curl`—but we don’t need to read its code (which is provided and commented for the curious).

- All errors have the same format: `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — **keys** for translation, never plain text;
- Authentication via a JWT token in an `httpOnly` / `sameSite=strict` cookie: the client-side JavaScript never sees the token;
- CSRF protection: `sameSite` cookie, and all POST requests must be in JSON;
- A “test mode” for the CAPTCHA so you can query the API with `curl`.

## The Case Study: The RdvMedecins Vue.js Client

A complete application for **scheduling appointments at a medical practice**, with **all** of its files (about forty) listed and commented.

- **Three roles**: `ADMIN` (manages doctors and clients), `DOCTOR` (schedules and cancels appointments), `USER` (the patient: books appointments for themselves, manages their account).
- **Privacy**: A patient never receives the names of other patients—the server does not send them.
- **The entire page state in the URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` reopens the booking window after pressing F5; the Previous/Next buttons work.
- **Server-side validation**: forms display errors returned by the API below each field; optimistic locking, duplicate names, username already taken, etc.
- **Session**: restored after pressing F5 (`GET /api/auth/moi`), expiration managed in a single location (401 response).
- **French / English**, confirmation window accessible via keyboard, Bootstrap 5.
- **Deployment**: the compiled client is served by the JSON server itself (same origin, no CORS).

## Technologies

Vue.js 3.5 (Composition API, `<script setup>`) · TypeScript 5.9 · Vite 7 · vue-router 4 · Pinia 3 · vue-i18n 11 · Bootstrap 5 · server-side: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Prerequisites

- A basic understanding of JavaScript (or TypeScript), HTML, and the HTTP protocol.
- Node.js 22 (or at least 20.19), Visual Studio Code with the Vue (Official) extension, and a MySQL server (e.g., Laragon on Windows) for the JSON server. Installation instructions are provided in the course appendices.

## Author

This course, its examples, the JSON server, and the case study were written by **Claude**, the AI from [Anthropic](https://www.anthropic.com) (September 2026), at the request of **Serge Tahé**.
