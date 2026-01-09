# Lean Canvas Innovation Platform

A comprehensive platform to support innovation management, learning, and AI-powered assistance. This project integrates three main components:

1. **LCI Tool** – A web application for filling Lean Canvas templates with checklists, guidance, and export functionality.
2. **Chatbot** – An AI assistant capable of answering questions about Lean Canvas templates and supporting the innovation process.
3. **Learning Management System (LMS)** – A platform to host courses, manage enrollments, and provide video tutorials related to Lean Canvas and innovation methodologies.

---

## Table of Contents

* Architecture
* Features
* Installation
* Environment Variables
* Docker Deployment
* Usage
* Contributing
* License

---

## Architecture

The platform is designed using a **microservices approach**, separating responsibilities across multiple components:

* **Web & LMS Backends** – Node.js/Express APIs handling business logic, data storage, and payments.
* **Chatbot Backend** – Python FastAPI service integrated with a vector database for AI-assisted answers.
* **Databases**:

  * **MongoDB** – Stores Lean Canvas templates, user accounts, and LMS data.
  * **Qdrant** – Vector database powering AI retrieval for the chatbot.
* **Frontends** – Static web applications deployed separately and connecting to the corresponding backend APIs.

All backend services run in **Docker containers**, allowing easy deployment and scaling.

---

## Features

### LCI Tool (Web App)

* Interactive Lean Canvas templates
* Checklists and guidance for each component
* Export filled canvases as Word documents
* User authentication

### Chatbot

* AI assistant for Lean Canvas guidance
* Vector search for fast and relevant answers
* Integrates with Qdrant for semantic search
* Accessible via backend API

### LMS

* Course listing and enrollment
* Video tutorials and learning materials
* Payment integration (Stripe/Easypaisa)
* Admin dashboard for course management

---

## Installation

### 1. Clone the repository

```bash
git clone <repo-url>
cd project-root
```

### 2. Install Dependencies

#### Web App Backend

```bash
cd backend
npm install
```

#### LMS Backend

```bash
cd lms/backend
npm install
```

#### Chatbot

```bash
cd chatbot
pip install -r requirements.txt
```

#### Frontends

```bash
cd frontend
npm install

cd ../lms/frontend
npm install
```

---

## Environment Variables

Each component requires its own `.env` file:

### Web Backend (`backend/.env`)

```
MONGO_URI=
JWT_SECRET=
STRIPE_KEY=
```

### LMS Backend (`lms/backend/.env`)

```
MONGO_URI=
PAYMENT_KEYS=
```

### Chatbot (`chatbot/.env`)

```
OPENAI_KEY=
QDRANT_URL=
QDRANT_API_KEY=
```

### Frontends (`frontend/.env`, `lms/frontend/.env`)

```
VITE_API_URL=<Web Backend URL>
VITE_LMS_API_URL=<LMS Backend URL>
```

> **Note:** Frontends must be rebuilt after updating environment variables.

---

## Docker Deployment

### EC2 #1 — Web & LMS Backend

```bash
cd deploy/ec2-app
docker compose up --build
```

Services:

* `web-backend` → port 5000
* `lms-backend` → port 4000

### EC2 #2 — Chatbot + Qdrant

```bash
cd deploy/ec2-ai
docker compose up --build
```

Services:

* `chatbot` → port 8000
* `qdrant` → port 6333

### Notes

* Frontends are **not part of EC2 deployment**. Deploy them to a static hosting service or CDN.
* Ensure **swap is enabled** on low-memory EC2 instances to prevent crashes.
* Use environment variables for all secrets; do not commit `.env` files.

---

## Usage

### Accessing Backends

* Web API: `http://<EC2_APP_IP>:5000`
* LMS API: `http://<EC2_APP_IP>:4000`
* Chatbot API: `http://<EC2_AI_IP>:8000`

### Frontend

* Rebuild frontend after updating `.env`
* Deploy to static hosting (Cloudflare Pages recommended)
* Ensure API URLs point to the correct EC2 backends

### Chatbot

* Connect via API calls from web app or LMS frontend
* Can query Lean Canvas templates and get AI-guided answers

---

## Contributing

* Fork the repository
* Create feature branch (`git checkout -b feature-name`)
* Commit changes (`git commit -m "description"`)
* Push (`git push origin feature-name`)
* Open a pull request

---

## License

This project is open-source and available under the MIT License.

```
```
