
# LoopBack 4 Backend Guide

**LoopBack 4** is a modern, _TypeScript-first_ backend framework for building APIs with **Node.js**. It is commonly used to create **REST APIs**, CRUD services, and enterprise-grade backend applications.

One of the biggest benefits of LoopBack 4 is that it provides a powerful **CLI** that can generate much of the boilerplate code for you. In many cases, you can create models, datasources, repositories, controllers, and relations without manually writing the initial files.

---

## 1. What is LoopBack 4?

**LoopBack 4** is an open-source Node.js framework that helps developers build structured and maintainable backend applications.

It provides built-in tools and conventions for:

- Creating **REST APIs**
- Defining **data models**
- Connecting to databases using **datasources**
- Accessing data through **repositories**
- Handling HTTP requests using **controllers**
- Generating **OpenAPI/Swagger documentation**
- Managing dependency injection
- Adding authentication and authorization
- Structuring large backend applications
- Generating common backend artifacts using the **LoopBack CLI**

LoopBack 4 is more opinionated than minimal frameworks like Express. It gives you a clear architecture and many helper tools out of the box.

A simple LoopBack 4 mental model:

```txt
HTTP Request
  -> Controller
  -> Service
  -> Repository
  -> Datasource
  -> Database
```

---

## CLI-First Development Benefit

LoopBack 4 is designed to be very productive with its CLI.

You can use the CLI to generate:

- A new LoopBack application
- Models
- Datasources
- Repositories
- Controllers
- Relation endpoints
- Example projects

This means you do **not** need to manually code every basic file from scratch.

For example, instead of manually creating a model file, writing decorators, defining properties, and wiring everything yourself, you can run:

```bash
lb4 model
```

Then answer a few prompts, and LoopBack will generate the model file for you.

You can also generate a full CRUD controller for a model and repository:

```bash
lb4 controller
```

After selecting the CRUD controller option, LoopBack can generate common endpoints such as:

```txt
POST   /users
GET    /users
GET    /users/{id}
PATCH  /users/{id}
PUT    /users/{id}
DELETE /users/{id}
```

This is one of the main advantages of LoopBack 4: it can automatically create a lot of standard backend code while still allowing you to customize the generated files later.

### Practical CLI Benefits

| Benefit | Explanation |
|---|---|
| **Fast scaffolding** | You can generate a new backend project in seconds. |
| **Less boilerplate** | You do not need to manually write basic models, repositories, or controllers. |
| **Consistent structure** | Generated files follow LoopBack conventions. |
| **Automatic wiring** | Generated artifacts are usually placed in the correct folders with the correct naming conventions. |
| **CRUD generation** | LoopBack can generate standard create, read, update, and delete endpoints. |
| **Relation generation** | You can generate relation endpoints between related models. |
| **OpenAPI support** | Generated controllers and decorators help LoopBack produce OpenAPI documentation. |
| **Customizable later** | You can edit generated files when you need custom logic. |

---

## 2. When to Use LoopBack 4

Use **LoopBack 4** when you need:

- A **structured TypeScript backend**
- A REST API with clear conventions
- CRUD endpoints for database models
- Auto-generated API documentation
- Dependency injection
- Repository-based data access
- A scalable project architecture
- Built-in CLI generators
- Enterprise-style extensibility
- Fast scaffolding without writing lots of boilerplate code

It is especially useful for:

- Admin dashboards
- SaaS backends
- Internal tools
- CRUD-heavy applications
- Data-driven APIs
- Microservices
- Teams that prefer strong conventions
- Projects where you want to generate standard resources quickly

LoopBack 4 is a strong choice when you want to move quickly while still keeping a clean backend architecture.

For example, if your webapp needs common resources like:

```txt
User
Post
Comment
Category
Order
Product
```

LoopBack can help you generate the basic model, repository, and controller structure for each resource without manually creating everything.

LoopBack 4 may **not** be the best choice if:

- You want a very minimal backend with almost no structure
- You prefer full manual control over every HTTP detail
- You are building a very small API with one or two endpoints
- Your team already has deep experience with another framework
- You primarily need GraphQL instead of REST

---

## 3. LoopBack 4 Project Structure

A typical LoopBack 4 project looks like this:

```txt
my-backend/
├── public/
├── src/
│   ├── controllers/
│   ├── datasources/
│   ├── models/
│   ├── repositories/
│   ├── services/
│   ├── observers/
│   ├── sequences/
│   ├── middleware/
│   ├── interceptors/
│   ├── utils/
│   ├── application.ts
│   ├── index.ts
│   ├── keys.ts
│   ├── migrate.ts
│   └── types.ts
├── __tests__/
├── dist/
├── package.json
└── tsconfig.json
```

---

### Folder and File Explanation

| Path | Purpose |
|---|---|
| `public/` | Contains static files such as HTML, CSS, images, or frontend assets. Often used if LoopBack serves a simple frontend or landing page. |
| `src/` | Main source code folder. All TypeScript backend code usually lives here. |
| `src/controllers/` | Contains controller classes. Controllers handle HTTP requests and define API routes such as `GET /users` or `POST /login`. You can create these manually or generate them using `lb4 controller`. |
| `src/models/` | Contains data models/entities. Models define the shape of your data, such as `User`, `Post`, or `Product`. You can create these manually or generate them using `lb4 model`. |
| `src/repositories/` | Contains repository classes. Repositories handle data access between models and datasources. You can generate them using `lb4 repository`. |
| `src/datasources/` | Contains database connection configurations. A datasource can connect to PostgreSQL, MySQL, MongoDB, in-memory storage, or other connectors. You can generate them using `lb4 datasource`. |
| `src/services/` | Contains business logic. Services are used when logic is more complex than basic CRUD operations. |
| `src/observers/` | Contains lifecycle observers. Observers run logic during application lifecycle events, such as application start or stop. |
| `src/sequences/` | Contains custom request sequences. A sequence defines the steps LoopBack performs when handling an HTTP request. |
| `src/middleware/` | Contains middleware functions. Middleware can handle cross-cutting concerns such as logging, CORS, rate limiting, or security headers. |
| `src/interceptors/` | Contains interceptors. Interceptors can run logic before or after controller, repository, or service method calls. |
| `src/utils/` | Contains reusable helper functions or utility classes. |
| `src/application.ts` | Defines the main LoopBack application class. This is where components, middleware, services, and boot options are often registered. |
| `src/index.ts` | Application entry point. This file usually creates and starts the LoopBack server. |
| `src/keys.ts` | Contains custom binding keys. Binding keys are used with LoopBack’s dependency injection container. |
| `src/migrate.ts` | Used for database schema migration or schema updates. |
| `src/types.ts` | Contains shared TypeScript types and interfaces. |
| `__tests__/` | Contains automated tests, such as unit tests and acceptance tests. |
| `dist/` | Contains compiled JavaScript output generated from TypeScript. This folder is usually generated during build. |
| `package.json` | Contains project dependencies, scripts, and metadata. |
| `tsconfig.json` | Contains TypeScript compiler configuration. |

---

### Important Naming Conventions

LoopBack often uses file naming conventions for automatic discovery.

Common conventions:

```txt
controllers/user.controller.ts
models/user.model.ts
repositories/user.repository.ts
datasources/db.datasource.ts
observers/startup.observer.ts
```

For example:

```txt
user.controller.ts    -> UserController
user.model.ts         -> User
user.repository.ts    -> UserRepository
db.datasource.ts      -> DbDataSource
```

These naming conventions help LoopBack automatically discover and register parts of your application.

Because the CLI follows these conventions automatically, using the CLI reduces the chance of naming or folder-structure mistakes.

---

## 4. Step-by-Step Installation Guide

### Step 1: Install Node.js

LoopBack 4 requires **Node.js** and **npm**.

It is recommended to use the latest **LTS** version of Node.js.

Check if Node.js is installed:

```bash
node -v
```

Check if npm is installed:

```bash
npm -v
```

If Node.js is not installed, download it from:

```txt
https://nodejs.org
```

---

### Step 2: Install the LoopBack CLI

Install the LoopBack command-line interface globally:

```bash
npm install -g @loopback/cli
```

Verify installation:

```bash
lb4 --version
```

The CLI is one of the main productivity features of LoopBack 4. It allows you to generate many parts of the backend without manually creating files.

---

### Step 3: Create a New LoopBack 4 Application

Create a new LoopBack project:

```bash
lb4 app my-backend
```

The CLI will ask a few questions. For a basic setup, you can usually accept the defaults.

Then move into the project folder:

```bash
cd my-backend
```

Install dependencies if they were not installed automatically:

```bash
npm install
```

At this point, you already have a working LoopBack backend structure without manually coding the base application.

---

### Step 4: Start the Development Server

Run the application:

```bash
npm start
```

Or, for development with automatic rebuilding:

```bash
npm run watch
```

Then open the app in your browser:

```txt
http://127.0.0.1:3000
```

Open the API explorer:

```txt
http://127.0.0.1:3000/explorer
```

You should see the LoopBack API explorer with available endpoints.

---

### Step 5: Generate a Model Using the CLI

Create a new data model:

```bash
lb4 model
```

Example model name:

```txt
User
```

Example properties:

```txt
email: string
name: string
createdAt: date
```

This will generate a file like:

```txt
src/models/user.model.ts
```

You do **not** need to manually create the model file or write the initial decorators yourself. LoopBack generates the basic model structure for you.

After generation, you can still edit the model manually if you need to add:

- Validation rules
- Relations
- Hidden properties
- Default values
- Indexes
- Custom settings

---

### Step 6: Generate a Datasource Using the CLI

Create a datasource to connect your app to a database:

```bash
lb4 datasource
```

Example datasource name:

```txt
db
```

For local testing, you can choose the in-memory connector:

```txt
memory
```

For real applications, you may use PostgreSQL, MySQL, MongoDB, or another database connector.

This will generate a file like:

```txt
src/datasources/db.datasource.ts
```

Again, you do not need to manually create the datasource file from scratch. The CLI generates the common structure for you.

---

### Step 7: Generate a Repository Using the CLI

Create a repository for your model:

```bash
lb4 repository
```

Choose:

```txt
Datasource: db
Model: User
Repository type: DefaultCrudRepository
```

This will generate a file like:

```txt
src/repositories/user.repository.ts
```

The generated repository connects your `User` model to the selected datasource.

This saves you from manually writing the repository class and injecting the datasource yourself.

---

### Step 8: Generate a Controller Using the CLI

Create a controller to expose HTTP endpoints:

```bash
lb4 controller
```

For simple CRUD APIs, choose:

```txt
REST CRUD controller
```

Then select:

```txt
User model
UserRepository
```

This will generate a controller like:

```txt
src/controllers/user.controller.ts
```

It may expose endpoints such as:

```txt
POST   /users
GET    /users
GET    /users/{id}
PATCH  /users/{id}
PUT    /users/{id}
DELETE /users/{id}
```

This is one of the biggest productivity benefits of LoopBack 4.

Instead of manually writing every route, request body schema, parameter decorator, and repository call, LoopBack can generate a working CRUD controller for you.

You can later customize the controller if you need custom endpoints such as:

```txt
POST /users/register
POST /users/login
GET  /users/me
POST /users/{id}/activate
```

---

### Step 9: Generate Relations Using the CLI

If your models are related, LoopBack can also help generate relation endpoints.

For example:

```txt
User has many Posts
Post belongs to User
```

You can use:

```bash
lb4 relation
```

This can help generate endpoints such as:

```txt
GET    /users/{id}/posts
POST   /users/{id}/posts
PATCH  /users/{id}/posts
DELETE /users/{id}/posts
```

This is useful when building relational APIs without manually wiring every relation endpoint.

---

### Step 10: Test the API

Restart the server if needed:

```bash
npm start
```

Then open the API explorer:

```txt
http://127.0.0.1:3000/explorer
```

You should see your generated CRUD endpoints available for testing.

This is especially useful because LoopBack automatically generates OpenAPI documentation for many of your endpoints.

---

### Step 11: Optional - Use PostgreSQL

If you want to use PostgreSQL instead of in-memory storage, install the PostgreSQL connector:

```bash
npm install loopback-connector-postgresql
```

Then create or update your datasource configuration.

Example datasource config:

```ts
const config = {
  name: 'db',
  connector: 'postgresql',
  host: process.env.DB_HOST,
  port: Number(process.env.DB_PORT ?? 5432),
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
};
```

Use environment variables in a `.env` file:

```txt
DB_HOST=localhost
DB_PORT=5432
DB_USER=your_database_user
DB_PASSWORD=your_database_password
DB_NAME=your_database_name
```

---

### Step 12: Build for Production

Build the TypeScript project:

```bash
npm run build
```

Run the compiled application:

```bash
node dist/index.js
```

For production, make sure to set:

```txt
NODE_ENV=production
```

Also configure environment variables for:

```txt
PORT
HOST
DB_HOST
DB_PORT
DB_USER
DB_PASSWORD
DB_NAME
JWT_SECRET
```

---

## Quick Command Reference

| Command | Description |
|---|---|
| `lb4 app` | Creates a new LoopBack 4 application |
| `lb4 model` | Generates a model without manually coding the initial file |
| `lb4 datasource` | Generates a datasource configuration file |
| `lb4 repository` | Generates a repository for a model |
| `lb4 controller` | Generates a controller, including optional CRUD controller generation |
| `lb4 relation` | Generates relation endpoints between models |
| `lb4 --help` | Shows available CLI commands |
| `npm start` | Starts the application |
| `npm run watch` | Starts in development mode with rebuilds |
| `npm run build` | Compiles TypeScript into JavaScript |
| `npm run migrate` | Runs database migration/schema update script |

---

## Example CLI Workflow

A common LoopBack workflow looks like this:

```bash
lb4 app my-backend
cd my-backend
lb4 model
lb4 datasource
lb4 repository
lb4 controller
npm start
```

With only a few commands, you can generate a working backend resource.

For example, to create a `User` resource, you can generate:

```txt
User model
db datasource
UserRepository
UserController
```

Then LoopBack can provide standard CRUD endpoints for the `User` resource.

This makes LoopBack 4 especially useful when you want to prototype quickly or build a backend with many standard database resources.

---

## Benefits of Using the LoopBack CLI

The LoopBack CLI gives you several important benefits:

- **You can create models without manually writing TypeScript model files**
- **You can create datasources without manually writing connector configuration files**
- **You can create repositories without manually wiring dependency injection**
- **You can create controllers without manually defining every CRUD route**
- **You can generate relation endpoints between related models**
- **You get consistent file naming conventions automatically**
- **You reduce boilerplate code**
- **You reduce human error**
- **You can scaffold features quickly**
- **You can still customize everything after generation**

In other words, LoopBack 4 is not only a backend framework. It is also a **code generation tool** that helps you build a standard backend faster.

---

## Summary

**LoopBack 4** is a powerful TypeScript backend framework for building structured REST APIs.

It is a good choice when you want:

- Strong project conventions
- CRUD generation
- OpenAPI documentation
- Repository-based data access
- Dependency injection
- Scalable backend architecture
- CLI-based scaffolding
- Less manual boilerplate code

A typical LoopBack backend separates concerns into:

```txt
controllers/   -> HTTP endpoints
models/        -> Data structures
repositories/  -> Data access
datasources/   -> Database connections
services/      -> Business logic
```

One of its biggest advantages is that you can use the **LoopBack CLI** to generate many common backend artifacts, including models, datasources, repositories, controllers, and relations, without manually coding everything from scratch.
