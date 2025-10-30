# 🧠 NeuralGuru Backend (`ng-backend`)

## Overview

`ng-backend` is the core backend service of the **NeuralGuru** platform — a virtual learning environment (VLE) that manages users, materials, assessments, tutor scheduling, analytics, and integrations with external microservices.

This service exposes RESTful APIs for the frontend applications and communicates with supporting microservices such as `ng-payment` for financial transactions.

---

## Architecture

- **Framework:** NestJS (Modular Monolith with microservice-ready design)
- **Database:** MongoDB (via Mongoose)
- **File Storage:** AWS S3
- **Microservices:**
  - `ng-payment` — external service handling payment processing and gateway integrations
  - Future services may include AI diagnostics or notification handlers

### High-Level Architecture

```bash
Frontend (Next.js / React Native)
       ↓
   ng-backend (Core API & Business Logic)
       ↓
   ├── ng-payment (Payment Service)
   └── Future Services (AI, Notifications, etc.)
```

---

## Core Capabilities

- Role-based authentication and authorization (Student, Tutor, Parent, Admin)
- Material management (upload and serve PDFs, videos, notes)
- Quiz and assessment system with score tracking
- Tutor profile management and session booking
- Performance analytics and report generation
- Secure integration with the `ng-payment` microservice for handling transactions

---

## Technology Stack

| Category            | Technology                                |
| ------------------- | ----------------------------------------- |
| Framework           | NestJS                                    |
| Language            | TypeScript                                |
| Database            | MongoDB                                   |
| Storage             | AWS S3                                    |
| Authentication      | JWT / Clerk / Auth.js                     |
| Communication       | REST (optionally gRPC / RabbitMQ)         |
| Reporting           | PDFKit, Recharts                          |
| Payment Integration | ng-payment (Stripe / Billplz / SenangPay) |

---

## Project Structure

```

ng-backend/
├── src/
│ ├── modules/
│ │ ├── auth/ # authentication & authorization
│ │ ├── users/ # user management
│ │ ├── materials/ # learning material uploads & access
│ │ ├── tests/ # quiz and assessment logic
│ │ ├── tutors/ # tutor profiles & scheduling
│ │ ├── bookings/ # booking system
│ │ ├── reports/ # analytics and report generation
│ │ └── payments/ # integration with ng-payment
│ ├── app.module.ts
│ └── main.ts
│
├── tests/
│ ├── e2e/ # end-to-end test cases
│ └── unit/ # unit tests
│
├── .env.example
├── package.json
├── tsconfig.json
└── README.md

```

---

## Integration with `ng-payment`

`ng-backend` communicates with the `ng-payment` microservice to handle all payment-related operations, including:

- Payment session creation and validation
- Transaction status updates
- Refunds and reconciliation

**Communication Pattern:**
Primarily via RESTful API (`/api/payments`), with optional support for asynchronous messaging (RabbitMQ or gRPC) in scalable environments.

---

## Getting Started

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/ng-backend.git
cd ng-backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

```bash
cp .env.example .env
```

### 4. Start Development Server

```bash
npm run start:dev
```

### 5. Build and Start Production Server

```bash
npm run build
npm run start:prod
```

### Run Tests

```bash
npm run test        # Unit tests
npm run test:e2e    # End-to-end tests
```
