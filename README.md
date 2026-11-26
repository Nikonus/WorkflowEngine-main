⚙️ WorkflowEngine

<p align="center">
  <strong>A Lightweight Workflow Orchestration Engine</strong>
  <br />
  Inspired by Temporal, Camunda, and AWS Step Functions.
</p><p align="center">
  <img src="https://img.shields.io/badge/Java-21-blue?logo=openjdk" />
  <img src="https://img.shields.io/badge/Spring%20Boot-4.0-green?logo=springboot" />
  <img src="https://img.shields.io/badge/Angular-19-red?logo=angular" />
  <img src="https://img.shields.io/badge/TypeScript-5.7-blue?logo=typescript" />
  <img src="https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql" />
  <img src="https://img.shields.io/badge/Architecture-DDD%20%7C%20CQRS%20%7C%20Hexagonal-purple" />
</p>---

📌 Overview

WorkflowEngine is a lightweight workflow orchestration system designed to define, execute, and monitor state-driven workflows.

The project implements enterprise software engineering principles, including Domain-Driven Design (DDD), Hexagonal Architecture, CQRS, and event-driven design.

It provides a backend workflow runtime engine alongside a reusable Angular component library and a demo application.

The primary objective is to explore how workflow orchestration systems are designed, structured, and implemented using modern Java and TypeScript technologies.

✨ Features

Backend Engine

- Define workflows with custom states and transitions.
- Create and manage workflow definitions.
- Start multiple workflow executions.
- Validate state transitions using domain rules.
- Maintain execution history.
- Support terminal states and execution lifecycle management.
- Immutable workflow execution model.
- Execution context through JSON metadata.

API & Integration

- RESTful API with CQRS separation.
- Workflow and execution management endpoints.
- Pagination for execution history and listings.
- API key authentication.
- Webhook callbacks for state changes.
- Swagger / OpenAPI documentation.
- Centralized exception handling.

Observability

- Prometheus metrics.
- Grafana dashboards.
- Micrometer integration.
- Structured JSON logging.
- Spring Boot Actuator endpoints.

Angular Frontend

- Workflow listing and management.
- Workflow creation and editing.
- Execution monitoring dashboard.
- Available transition controls.
- Execution history timeline.
- Search and pagination.
- Loading skeletons and error handling.
- Reusable standalone Angular components.
- Signal-based state management.
- Customizable CSS design system.

🏗️ Architecture

The project follows a layered, modular architecture.

                    Angular Frontend
                           |
                           v
                      REST API
                           |
                           v
                   Application Layer
                   /               \
              Commands            Queries
                   \               /
                           |
                           v
                     Domain Layer
                           |
                  WorkflowEngine
                           |
                 Domain Events
                           |
                           v
                 Infrastructure Layer
                   /             \
              Persistence      Event Adapters
                   |                 |
              PostgreSQL       Spring Events

Architectural Principles

Principle| Implementation
DDD| Domain models, aggregates, value objects
Hexagonal Architecture| Ports and adapters
CQRS| Separate command and query use cases
Event-Driven Design| Domain event publishing
Immutability| Immutable workflow executions
Persistence Ignorance| Domain independent of JPA
Dependency Inversion| Infrastructure implements application ports

🧠 Core Domain Concepts

1. Workflow

A workflow represents a definition containing:

- Unique workflow identity.
- Available states.
- Allowed transitions.
- Initial state.

2. WorkflowExecution

An execution represents a running instance of a workflow.

It maintains:

- Execution identity.
- Current state.
- Associated workflow ID.
- Execution context.
- State transition history.

3. WorkflowEngine

The central domain service responsible for:

- Validating requested transitions.
- Enforcing workflow rules.
- Producing updated execution instances.
- Generating domain events.

🔄 CQRS Implementation

The application separates write operations from read operations.

Commands

- CreateWorkflow
- UpdateWorkflow
- DeleteWorkflow
- StartWorkflowExecution
- ExecuteTransition

Queries

- ListWorkflows
- GetWorkflow
- GetExecution
- ListExecutions
- GetNextStates
- GetHistory

📂 Project Structure

WorkflowEngine/
│
├── backend/
│   ├── api/
│   │   ├── controller/
│   │   ├── dto/
│   │   ├── exception/
│   │   └── mapper/
│   │
│   ├── application/
│   │   ├── facade/
│   │   ├── port/
│   │   └── usecase/
│   │       ├── commands/
│   │       └── queries/
│   │
│   ├── domain/
│   │   ├── event/
│   │   ├── exception/
│   │   ├── model/
│   │   └── service/
│   │
│   ├── infrastructure/
│   │   ├── event/
│   │   ├── persistence/
│   │   └── config/
│   │
│   └── docs/
│
├── frontend/
│   └── projects/
│       ├── workflow-engine/
│       │   └── src/lib/
│       │       ├── models/
│       │       ├── config/
│       │       ├── services/
│       │       └── components/
│       │
│       └── shell/
│           └── src/app/
│
├── docs/
│   ├── CONTEXT.md
│   ├── mvp.md
│   ├── roadmap.md
│   └── features/
│
└── docker-compose.yml

🛠️ Technology Stack

Category| Technology
Language| Java 21
Backend Framework| Spring Boot 4.0.6
Frontend Framework| Angular 19.2
Programming Language| TypeScript 5.7
Database| PostgreSQL 16
In-memory Database| H2
ORM| Spring Data JPA
Database Migration| Flyway
Build System| Gradle Kotlin DSL
Reactive Programming| RxJS 7
Frontend State| Angular Signals
API Documentation| Springdoc OpenAPI
Authentication| API Key
Monitoring| Prometheus + Grafana
Metrics| Micrometer
Backend Testing| JUnit 5, Mockito
Integration Testing| Testcontainers
Frontend Testing| Jasmine, Karma
Infrastructure| Docker Compose

🚀 Getting Started

Prerequisites

Make sure you have installed:

- Java 21 or later
- Node.js 20 or later
- npm
- Docker Desktop
- Git

1. Clone the Repository

git clone https://github.com/YOUR_USERNAME/WorkflowEngine.git

cd WorkflowEngine

2. Start PostgreSQL

docker compose up -d

3. Start Backend

cd backend

./gradlew bootRun --args='--spring.profiles.active=dev-pg'

Backend runs at:

"http://localhost:8080"

4. Start Frontend

Open another terminal:

cd frontend

npm install

ng serve

Frontend runs at:

"http://localhost:4200"

5. API Documentation

Once the backend is running, access Swagger UI:

"http://localhost:8080/swagger-ui.html"

🧪 Testing

Backend Tests

cd backend

./gradlew test

Frontend Tests

cd frontend

ng test

PostgreSQL Integration Tests

The PostgreSQL integration tests use Testcontainers and require Docker to be running.

📊 Workflow Lifecycle

A typical workflow execution follows this sequence:

Create Workflow
      |
      v
Start Execution
      |
      v
Initial State
      |
      v
Request Transition
      |
      v
Validate Transition
      |
      v
Update Execution
      |
      v
Publish Domain Event
      |
      v
Record Execution History
      |
      v
Terminal State?
   /       \
 No         Yes
 |           |
 v           v
Continue   Completed

🗺️ Roadmap

- [x] Core workflow domain model
- [x] State transition validation
- [x] Workflow execution lifecycle
- [x] CQRS-based application layer
- [x] REST API
- [x] PostgreSQL persistence
- [x] Domain event publishing
- [x] Angular workflow interface
- [x] Execution history
- [x] Prometheus metrics and Grafana integration
- [ ] Durable event processing
- [ ] Distributed workflow execution
- [ ] Retry and timeout policies
- [ ] Scheduled workflow execution
- [ ] Advanced workflow visualization
- [ ] Multi-tenant support

🎯 Project Motivation

I built WorkflowEngine to deepen my understanding of enterprise backend engineering and workflow orchestration.

Rather than building another basic CRUD application, I wanted to explore:

- How complex business processes can be modeled as state machines.
- How to separate domain logic from infrastructure.
- How CQRS improves separation of responsibilities.
- How domain events enable event-driven integrations.
- How to design reusable frontend libraries.
- How to test backend systems across multiple architectural layers.
- How monitoring and observability fit into production-oriented applications.

This project is an ongoing exploration of backend architecture, distributed systems, and full-stack engineering.

👨‍💻 Author

Nikhil Dubey

Full Stack Developer | Java | Spring Boot | Angular | React

---

<p align="center">
  Built with Java, Spring Boot, Angular, and a passion for software engineering.
  <br />
  ⭐ If you find this project useful, consider giving it a star!
</p>
