# ⚙️ CREDBUD Backend API Server

> A modular Node.js and Express REST API powering CREDBUD's authentication, user management, attendance, grants, subjects, posts, and administrative operations.

![Node.js](https://img.shields.io/badge/Node.js-22.16.0-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-4.18.2-000000?logo=express&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6%2B-F7DF1E?logo=javascript&logoColor=black)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?logo=firebase&logoColor=black)
![API](https://img.shields.io/badge/API-REST-blue)
![License](https://img.shields.io/badge/License-ISC-lightgrey)

## 📖 Overview

**CREDBUD Backend API Server** is the server-side component of the CREDBUD application. Built with Node.js and Express.js, it organizes application endpoints into separate route modules and uses middleware, controllers, and utility functions to manage request processing.

The backend provides route groups for authentication, users, attendance, grants, subjects, posts, and administration. Its dependencies also support Firebase integration, Google APIs, JWT-based authentication, password hashing, scheduled tasks, and OTP-related functionality.

This repository is maintained independently from the frontend.

**Related repositories**

- Backend API: [CREDBUD-BACKEND-API-Server](https://github.com/pratikabhang/CREDBUD-BACKEND-API-Server)
- Frontend application: [CREDBUD-FRONTEND](https://github.com/pratikabhang/CREDBUD-FRONTEND)

## ✨ Features

- **REST API Architecture:** Organizes HTTP endpoints into dedicated modules.
- **Authentication Support:** Includes JWT, password-hashing, and OTP-related dependencies.
- **User Management:** Provides a dedicated user route group.
- **Attendance Management:** Separates attendance-related API operations.
- **Grant Management:** Organizes grant-related functionality.
- **Subject and Post Management:** Maintains separate route groups for subjects and posts.
- **Administrative APIs:** Provides a dedicated admin route group.
- **Firebase Integration:** Includes Firebase and Firebase Admin SDK dependencies.
- **Google API Integration:** Includes the Google APIs client library.
- **Scheduled Tasks:** Uses `node-cron` for scheduling recurring jobs.
- **Reusable Middleware:** Uses request parsing, cookies, CORS, and logging middleware.
- **Environment-Specific Startup:** Provides separate development and production startup commands.

The exact behavior of individual authentication flows, API operations, and scheduled tasks depends on the implementation in the source code.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Node.js 22.16.0 | JavaScript runtime |
| Express.js 4.x | HTTP server and routing |
| JavaScript | Backend application logic |
| Firebase | Firebase service integration |
| Firebase Admin SDK | Server-side Firebase operations |
| Google APIs | Google service integrations |
| JSON Web Token | Token-based authentication support |
| bcrypt / bcryptjs | Password hashing libraries |
| dotenv | Environment configuration |
| CORS | Cross-origin request configuration |
| cookie-parser | Cookie parsing |
| Morgan | HTTP request logging |
| node-cron | Scheduled jobs |
| Speakeasy | OTP functionality |
| Nodemon | Development server restart |
| cross-env | Cross-platform environment variables |

Refer to `package.json` for the exact dependency versions.

## 🏗️ Architecture

```text
                 Frontend Client
                       |
                       v
                  Express App
                       |
                       v
                Middleware Layer
                       |
                       v
                   API Routes
                       |
       +---------------+----------------+
       |        |       |       |        |
       v        v       v       v        v
     Users     Auth  Attendance Grants  Admin
       |        |       |       |        |
       +--------+-------+-------+--------+
                       |
                       v
                   Controllers
                       |
                       v
                 Utility Modules
                       |
              +--------+--------+
              |                 |
              v                 v
          Firebase           Google APIs
```

The diagram illustrates the modular design and available integrations; actual data flow depends on the individual route handlers and controllers.

## 🛣️ API Route Groups

| Route prefix | Purpose |
|---|---|
| `/api/v1/user` | User management |
| `/api/v1/auth` | Authentication |
| `/api/v1/attendance` | Attendance operations |
| `/api/v1/grant` | Grant operations |
| `/api/v1/admin` | Administrative operations |
| `/api/v1/subjects` | Subject management |
| `/api/v1/posts` | Post management |

These prefixes identify registered route groups. Inspect `routes/` and `controllers/` for individual endpoints, supported HTTP methods, payloads, and authentication requirements.

## 📂 Project Structure

```text
CREDBUD-BACKEND-API-Server/
├── .netlify/
├── controllers/
├── middleware/
├── routes/
├── utils/
├── app.js
├── package.json
├── .node-version
├── .envbak
├── cert.pem
├── key.pem
├── appmap.yml
├── .gitignore
└── .gitattributes
```

- `app.js` — Express application entry point.
- `routes/` — API route definitions.
- `controllers/` — Request-handling logic.
- `middleware/` — Shared request-processing middleware.
- `utils/` — Utility functions.
- `package.json` — Dependencies and npm scripts.
- `.node-version` — Node.js version specification.

## 🎯 Scope and Objectives

### In scope

- Organizing backend API endpoints.
- Supporting authentication-related functionality.
- Providing modular user, attendance, grant, subject, post, and admin routes.
- Integrating configured external services.
- Supporting development and production startup workflows.

### Out of scope

- Frontend UI implementation.
- Browser-side routing and presentation.
- Client-side charts, QR scanning, and calendar components.
- Frontend deployment configuration.

These responsibilities belong to the separate frontend repository or the relevant external services.

## 💻 Prerequisites

- Node.js 22.16.0
- npm
- Git
- Required environment variables and service credentials
- Valid development TLS certificates if required by the non-production startup configuration

Check your versions:

```bash
node --version
npm --version
```

## 🚀 Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/pratikabhang/CREDBUD-BACKEND-API-Server.git
cd CREDBUD-BACKEND-API-Server
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a local `.env` file containing the variables required by the application.

Example startup configuration:

```env
NODE_ENV=development
PORT=443
```

These example values are not a complete configuration. Review `app.js`, the controllers, and the integration code for the actual required variables.

Never commit credentials, tokens, or private keys.

### 4. Configure development HTTPS

The development configuration references `cert.pem` and `key.pem`. Ensure valid local development certificate files are available at the paths expected by the application.

Never use an exposed production private key.

### 5. Start development

```bash
npm run dev
```

This runs the application through Nodemon when configured in `package.json`.

### 6. Start production

```bash
npm start
```

The production script sets the production environment and starts `app.js`. Configure the deployment port and required service credentials in the hosting environment.

## ▶️ API Usage

### Root health check

```http
GET /
```

Example response:

```json
{
  "message": "SERVER IS RUNNING. Try /api/v1/test"
}
```

### API health check

```http
GET /api/v1/test
```

Example response:

```json
{
  "message": "CREDBUD SERVER IS RUNNING"
}
```

### Test with cURL

For a locally running HTTPS server with a trusted development certificate:

```bash
curl https://localhost:443/
```

```bash
curl https://localhost:443/api/v1/test
```

Use the configured port if it differs from `443`.

## ⚙️ Environment Configuration

Depending on the enabled features, the application may require:

- `NODE_ENV` — startup environment.
- `PORT` — listening port.
- Firebase credentials — for server-side Firebase operations.
- Google API credentials — for enabled Google integrations.
- TLS certificate and key — for the development HTTPS configuration.

This is a configuration overview, not an exhaustive list of environment variables. Confirm exact names and requirements in the source code.

## 🔐 Security

- Keep production credentials and authentication secrets out of Git.
- If a real private key has been exposed, replace it and review repository history.
- Enforce authorization on protected endpoints.
- Validate request bodies and query parameters.
- Configure CORS for trusted frontend origins.
- Protect Firebase and Google service credentials.
- Use secure cookie attributes where applicable.
- Review dependencies for known vulnerabilities.
- Use HTTPS and appropriate production error handling.

## 🧪 Testing

Review the scripts in `package.json` before running tests. If an automated test suite is not configured, manually test the health checks and relevant API endpoints using a REST client.

Automated unit and integration tests are recommended for route handlers, middleware, authentication, and external service integrations.

## 🔮 Future Improvements

- Add OpenAPI/Swagger documentation.
- Introduce automated unit and integration tests.
- Provide a sanitized `.env.example`.
- Standardize API error responses.
- Add centralized request validation and error handling.
- Document authentication flows and API payloads.
- Improve production logging and monitoring.
- Add CI checks for tests and dependency security.
- Review exposed certificate files and deployment configuration.

These are proposed improvements, not claims about existing functionality.

## 🤝 Contributing

1. Fork the repository.
2. Clone your fork:

   ```bash
   git clone https://github.com/<your-username>/CREDBUD-BACKEND-API-Server.git
   cd CREDBUD-BACKEND-API-Server
   ```

3. Create a branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

4. Make and test your changes.
5. Commit your work:

   ```bash
   git add .
   git commit -m "Improve backend API functionality"
   ```

6. Push your branch:

   ```bash
   git push origin feature/your-feature-name
   ```

7. Open a pull request with a description of the changes and tests performed.

Do not include credentials, private keys, or sensitive environment files in contributions.

## 📄 License

The project's `package.json` specifies the **ISC License**. Review the repository's license files and preserve applicable third-party notices.

## 👨‍💻 Author

**Pratik Abhang**

- GitHub: [@pratikabhang](https://github.com/pratikabhang)
- Backend: [CREDBUD-BACKEND-API-Server](https://github.com/pratikabhang/CREDBUD-BACKEND-API-Server)
- Frontend: [CREDBUD-FRONTEND](https://github.com/pratikabhang/CREDBUD-FRONTEND)

---

⭐ If you find this project useful, consider starring the repository.

*Secure APIs. Modular architecture. Reliable backend development.*
