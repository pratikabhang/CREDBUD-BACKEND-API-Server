# ⚙️ cREDBUD-BACKEND-API-ServeR

> A Node.js and Express backend providing REST API endpoints for user management, authentication, attendance, grants, subjects, posts, and administrative operations.

![Node.js](https://img.shields.io/badge/Node.js-22.16.0-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-Backend-000000?logo=express&logoColor=white)
![REST API](https://img.shields.io/badge/API-REST-blue)
![Environment](https://img.shields.io/badge/Environment-Node.js-green)
![License](https://img.shields.io/badge/License-Not%20Specified-lightgrey)

## 📖 Overview

**BACKEND** is a Node.js backend project built using Express.js. The application exposes REST API routes for several modules, including user management, authentication, attendance, grants, subjects, posts, and administration.

The codebase uses middleware for JSON request parsing, cookie handling, cross-origin resource sharing (CORS), request logging, and user-type checks. It also includes HTTPS server configuration for non-production environments and a separate production startup path.

The repository provides the server-side foundation for the **CREDBUD** application, as indicated by its API health-check response.

🔗 **GitHub Repository:** [pratikabhang/BACKEND](https://github.com/pratikabhang/BACKEND)

## ✨ Features

- **User Management:** Provides a dedicated route group for user-related operations.
- **Authentication:** Separates authentication endpoints from other application routes.
- **Attendance Management:** Exposes endpoints through a dedicated attendance route group.
- **Grant Management:** Organizes grant-related API operations separately.
- **Subject Management:** Provides routes for subject-related operations.
- **Posts and Administration:** Includes dedicated post and admin route groups.
- **Middleware Integration:** Uses Express middleware for request parsing, cookies, CORS, and logging.
- **HTTPS Development Support:** Configures an HTTPS server for non-production execution.
- **Environment-Based Startup:** Selects the server startup behavior based on `NODE_ENV`.

The specific endpoint methods, authorization rules, database operations, and request schemas depend on the implementation in the corresponding route and controller files.

## 🛠️ Tech Stack

![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-000000?logo=express&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![npm](https://img.shields.io/badge/npm-CB3837?logo=npm&logoColor=white)

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| Express.js | HTTP server and routing |
| dotenv | Loads environment variables |
| cors | Configures cross-origin resource sharing |
| cookie-parser | Parses cookies from incoming requests |
| Morgan | HTTP request logging |
| Node.js `https` module | Creates an HTTPS server |
| Node.js `fs` module | Reads certificate and key files |
| Netlify configuration | Deployment-related configuration present in the repository |

The repository's `.node-version` specifies **Node.js 22.16.0**. The complete dependency list and versions should be taken from `package.json` and the available lockfile, if any.

## 🏗️ Architecture

The backend follows a modular Express.js architecture that separates route definitions, controllers, middleware, and utility functions.

```text
                 Client Application
                        |
                        v
                   Express App
                        |
                        v
                 Middleware Layer
           +------------+-------------+
           |            |             |
           v            v             v
         CORS        JSON Parser   Cookie Parser
           |            |             |
           +------------+-------------+
                        |
                        v
                   API Router
                        |
      +-----------------+------------------+
      |          |          |               |
      v          v          v               v
    Users      Auth     Attendance       Grants
      |          |          |               |
      +----------+----------+---------------+
                        |
                        v
                    Controllers
                        |
                        v
                   Application Logic
```

### API Route Groups

The application registers the following route prefixes in `app.js`:

| Route prefix | Module |
|---|---|
| `/api/v1/user` | User management |
| `/api/v1/auth` | Authentication |
| `/api/v1/attendance` | Attendance |
| `/api/v1/grant` | Grants |
| `/api/v1/admin` | Administrative operations |
| `/api/v1/subjects` | Subject management |
| `/api/v1/posts` | Posts |

These prefixes identify route groups, not a complete list of individual endpoints.

## 🎯 Project Objectives

- Provide a modular backend for the CREDBUD application.
- Separate API route definitions from request-handling logic.
- Organize application features into maintainable modules.
- Support environment-specific server configuration.
- Apply reusable middleware for common HTTP concerns.
- Provide health-check endpoints for basic server availability testing.

## 📂 Project Structure

```text
BACKEND/
├── .netlify/          # Netlify-related configuration
├── controllers/       # Request-handling logic
├── middleware/        # Request-processing middleware
├── routes/            # API route definitions
├── utils/             # Shared utility functions
├── app.js             # Express application entry point
├── package.json       # Project metadata and dependencies
├── .node-version      # Node.js version specification
├── .envbak            # Environment-related backup file
├── cert.pem           # SSL certificate file
├── key.pem            # SSL private key file
├── appmap.yml         # Application mapping configuration
├── .gitignore         # Git ignore rules
└── .gitattributes     # Git file-handling configuration
```

**Security note:** The repository listing includes `key.pem` and `cert.pem`. Never publish a real production private key. If `key.pem` contains an actual private key that has been exposed publicly, replace it and review the repository history.

## 💻 Prerequisites

Before running the backend, install:

- [Node.js 22.16.0](https://nodejs.org/)
- npm, included with Node.js
- Git
- Valid local TLS certificate and private key files if using the non-production HTTPS startup path

Check the installed versions:

```bash
node --version
npm --version
```

The Node.js version should match the version specified in `.node-version`.

## 🚀 Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/pratikabhang/BACKEND.git
cd BACKEND
```

### 2. Install Dependencies

```bash
npm install
```

This installs the dependencies declared in `package.json`.

### 3. Configure Environment Variables

The application loads environment variables through `dotenv`.

Create a local `.env` file using the variable names required by the application:

```env
NODE_ENV=development
PORT=443
```

These values illustrate the startup configuration visible in `app.js`. Review the route handlers, controllers, and configuration before adding any database credentials, authentication secrets, or other variables.

Do not commit `.env` files containing sensitive values.

### 4. Configure HTTPS for Local Development

The non-production startup path reads:

```text
key.pem
cert.pem
```

Ensure valid local certificate and private key files exist at the paths expected by `app.js`.

For local development, use certificates appropriate for your development environment. Never use a publicly exposed private key in production.

### 5. Start the Server

Inspect `package.json` to confirm the available npm scripts. If no suitable start script exists, the application entry point can be run directly:

```bash
node app.js
```

The server uses HTTPS in non-production mode and listens on the configured `PORT`, defaulting to `443`. In production mode, it uses `app.listen()` with `process.env.PORT`.

**Important:** Set the environment variables and certificate files correctly before starting the application.

## ▶️ API Usage

### Health Check

The application defines a root endpoint for checking server availability.

**Request**

```http
GET /
```

**Example response**

```json
{
  "message": "SERVER IS RUNNING. Try /api/v1/test"
}
```

### API Test Endpoint

**Request**

```http
GET /api/v1/test
```

**Example response**

```json
{
  "message": "CREDBUD SERVER IS RUNNING"
}
```

These health-check endpoints are defined directly in `app.js`.

### Available API Route Prefixes

The application registers the following API groups:

```text
/api/v1/user
/api/v1/auth
/api/v1/attendance
/api/v1/grant
/api/v1/admin
/api/v1/subjects
/api/v1/posts
```

To identify the available HTTP methods, parameters, request bodies, and responses for each route, inspect the files in `routes/` and their associated controllers.

## 🔧 Development

### Check Installed Dependencies

```bash
npm ls --depth=0
```

### Check Node.js Version

```bash
node --version
```

### Inspect Server Logs

Morgan is configured with the `tiny` logging format, which records HTTP request information in the server output.

### Test API Endpoints

Use a REST client such as Postman, Insomnia, or `curl` to test the health-check endpoints and the application routes.

For example, if the local HTTPS server is running with a trusted development certificate:

```bash
curl https://localhost:443/api/v1/test
```

If your development certificate is self-signed, configure trust for that certificate in your development environment instead of disabling TLS verification as a general practice.

## 🔐 Security Considerations

Before deploying this backend publicly:

- Keep production credentials and authentication secrets outside source control.
- Replace any exposed private keys and rotate affected credentials.
- Validate incoming request bodies and query parameters.
- Apply authentication and authorization to protected endpoints.
- Restrict CORS origins to trusted frontend applications.
- Disable verbose development behavior in production.
- Configure HTTPS and secure cookie attributes appropriately.
- Review dependency vulnerabilities regularly.
- Ensure `NODE_ENV` and `PORT` are configured correctly for the deployment platform.

## 🚀 Future Improvements

Potential improvements include:

- Document all API endpoints with OpenAPI/Swagger.
- Add automated unit and integration tests.
- Provide a sanitized `.env.example`.
- Add structured error handling and consistent API response formats.
- Introduce request validation for each route.
- Add centralized logging and monitoring.
- Configure a repeatable deployment workflow.
- Add health checks suitable for production monitoring.
- Document database technology and schemas after confirming the implementation.

These are suggested enhancements, not claims about existing functionality.

## 🤝 Contributing

Contributions and improvements are welcome.

1. Fork the repository.
2. Clone your fork:

   ```bash
   git clone https://github.com/<your-username>/BACKEND.git
   cd BACKEND
   ```

3. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

4. Make your changes in the relevant routes, controllers, middleware, or utilities.
5. Test the affected API behavior.
6. Commit your changes:

   ```bash
   git add .
   git commit -m "Improve backend functionality"
   ```

7. Push the branch:

   ```bash
   git push origin feature/your-feature-name
   ```

8. Open a pull request explaining the changes and tests performed.

## 📄 License

No repository-wide license has been confirmed. Until a `LICENSE` file is added, do not assume that the code may be freely redistributed or reused.

## 👨‍💻 Author

**Pratik Abhang**

- GitHub: [@pratikabhang](https://github.com/pratikabhang)
- Repository: [BACKEND](https://github.com/pratikabhang/BACKEND)

---

⭐ If you find this project useful, consider starring the repository.

*Modular APIs. Clear separation of concerns. Maintainable backend development.*
