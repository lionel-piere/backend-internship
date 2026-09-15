# Backend Internship Days 1–2 Exercise

- **Intern:** Lionel Piere Punsalang
- **Current Role:** Software Developer Intern at Tito Solutions
- **Starter Repository Source:** [Official NestJS TypeScript Starter](https://github.com/nestjs/typescript-starter)
- **Internship Repository:** [backend-internship](https://github.com/lionel-piere/backend-internship)
- **Feature Branch:** `feat/day1-2-nestjs-introduction`

---

## Exercise Overview
This exercise establishes the core backend foundations for Days 1–2 of the Tito Solutions Internship Curriculum:
1. Cloning, configuring, and running the official NestJS starter application.
2. Understanding NestJS architectural components (Modules, Controllers, Services, Dependency Injection).
3. Tracing and implementing the HTTP request lifecycle: **Client Request → Controller → Injected Service → HTTP 200 Response**.
4. Personalizing the root endpoint (`GET /`) greeting to return:
   ```text
   Hello from Lionel Piere Punsalang!
   ```
5. Updating both unit and end-to-end (e2e) test suites to assert the personalized greeting.
6. Ensuring code quality through formatting, linting, test suites, and production build checks.

---

## Environment & Node.js Compatibility

- **Supported Node Versions:** `^22.22.3 || ^24.15.0 || >=26.0.0` (recommended by the starter tooling in `package-lock.json`).
- **Verified Local Environment:** Node `v24.12.0` and npm `11.6.2` on Windows (all scripts, builds, and test suites run and pass successfully).

---

## How the NestJS Architecture Works

NestJS follows a modular, layer-separated architecture with Dependency Injection (DI):

| File Path | Role | Description |
| :--- | :--- | :--- |
| `src/main.ts` | **Application Bootstrap** | Entry point of the server. Uses `NestFactory.create(AppModule)` to instantiate the application and begins listening on port 3000. |
| `src/app.module.ts` | **Root Module** | The central organizer of the application. It registers `AppController` and provides `AppService` to the NestJS Dependency Injection container. |
| `src/app.controller.ts` | **Request Controller** | Handles incoming HTTP requests for defined routes (`@Get('/')`). It receives `AppService` via constructor injection and delegates business logic to it. |
| `src/app.service.ts` | **Service Provider** | Implements the business logic. `getHello()` supplies the personalized greeting string: `"Hello from Lionel Piere Punsalang!"`. |
| `src/app.controller.spec.ts` | **Unit Test Suite** | Tests the controller with `AppService` and checks the returned greeting. |
| `test/app.e2e-spec.ts` | **End-to-End Test Suite** | Boots a simulated NestJS test application and executes a full HTTP request via Supertest, asserting an HTTP 200 status and the personalized greeting. |

### Request Lifecycle
```
Client (Postman / Thunder Client / Browser)
                    │
                    ▼  HTTP GET http://localhost:3000/
          src/app.controller.ts
                    │
                    ▼  Calls injected this.appService.getHello()
           src/app.service.ts
                    │
                    ▼  Supplies "Hello from Lionel Piere Punsalang!"
HTTP 200 OK ◄───────┘
```

---

## Setup & Running Instructions

### 1. Install Dependencies
```bash
npm install
```

### 2. Run the Development Server
```bash
npm run start:dev
```
The application will be live at `http://localhost:3000/`.

### 3. Build for Production
```bash
npm run build
```

---

## Testing with Postman or Thunder Client

1. Open **Thunder Client** (in your editor) or **Postman**.
2. Create a new request:
   - **Method:** `GET`
   - **URL:** `http://localhost:3000/`
3. Click **Send**.
4. Expected Response:
   - **Status:** `200 OK`
   - **Body:** `Hello from Lionel Piere Punsalang!`

---

## Verification & Quality Checks

Run the following commands from the project root:

- **Formatting Check & Fix:**
  ```bash
  npm run format
  ```
- **Linting Check:**
  ```bash
  npm run lint
  ```
- **Unit Tests:**
  ```bash
  npm run test
  ```
- **End-to-End (E2E) Tests:**
  ```bash
  npm run test:e2e
  ```
- **Production Build:**
  ```bash
  npm run build
  ```

> **Note on test output:** All unit and e2e test assertions pass (`1 passed (1)`). Any printed notices during test execution (such as the Vite path resolution migration notice or the Observe telemetry notice on test shutdown) are upstream package logs and do not indicate application failure.

---

## Original Attribution & License

This project is built upon the official [NestJS TypeScript Starter](https://github.com/nestjs/typescript-starter) created by [Kamil Myśliwiec](https://twitter.com/kammysliwiec) and the NestJS contributors.

- **License:** [MIT](https://github.com/nestjs/nest/blob/master/LICENSE)
