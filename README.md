## Hi, I'm Roman
### Python Backend Developer | FastAPI · Django · PostgreSQL | AI/LLM Integrations

I build backend systems, APIs, and integrations for business applications. My experience includes commercial CRM development and independently building and maintaining production e-commerce and B2B platforms.

I focus on reliable business logic, database performance, asynchronous processing, external integrations, and maintainable architecture.

---

## About Me

- Commercial experience developing Python backends for CRM and business applications.
- Build and maintain production applications with FastAPI, Django, PostgreSQL, and Redis.
- Design REST APIs, database schemas, background processing, payment workflows, and external service integrations.
- Have hands-on project experience integrating LLMs, building RAG pipelines, and implementing vector search.
- Handle the full development cycle: architecture, implementation, testing, Docker deployment, and production support.

---

## Tech Stack

- **Backend:** Python, FastAPI, Django, Django REST Framework, SQLAlchemy, Pydantic, asyncio
- **Databases & Search:** PostgreSQL, Redis, Qdrant, FAISS
- **Background Processing:** RQ, ARQ, async workers, scheduled jobs
- **Integrations:** REST API, HTTPX, aiohttp, Playwright, aiogram
- **AI / LLM:** LangChain, LiteLLM, RAG, embeddings, vector search, DeepSeek, OpenRouter, Ollama
- **Infrastructure:** Docker, Docker Compose, Linux, Nginx, GitHub Actions, GitLab CI/CD
- **Engineering:** pytest, Alembic, Ruff, OpenAPI, Git

---

## Featured Projects

### [Shopstore](https://github.com/MrGrose/Shopstore)
*Production e-commerce backend for a sports equipment store.*
- Built and maintain a store with approximately 13,000 products on the storefront and 17,000 product records in the database.
- Designed the backend with FastAPI, async SQLAlchemy, PostgreSQL, Redis, and RQ.
- Implemented order processing, inventory availability, supplier integrations, and delivery tracking.
- Integrated SBP QR payments with idempotent callbacks and payment status reconciliation.
- Implemented reliable background notifications using the transactional outbox pattern.
- Added concurrency control for catalog imports, order creation, and inventory operations.
- Built an admin interface and Telegram Mini App on top of the same backend.
- Deployed and maintain the application using Docker Compose.

### [B2B-Commerce](https://github.com/MrGrose/B2B-commerce)
*B2B wholesale commerce platform.*
- Designed a modular monolith with FastAPI, async SQLAlchemy, and PostgreSQL.
- Implemented company accounts, product catalog, invoices, inventory, payments, and financial reports.
- Built inventory reservations with PostgreSQL row-level locking to prevent overselling.
- Implemented idempotent payment operations and invoice expiration workflows.
- Added audit logging, authentication, and security controls.
- Configured background jobs with ARQ and Redis.
- Set up CI/CD with GitHub Actions and automated deployment to a VPS.

### [Video Analytics Bot](https://github.com/MrGrose/video-analytics-bot)
*Telegram bot for querying analytics using natural language.*
- Integrated DeepSeek to convert natural-language questions into SQL queries.
- Connected the bot to PostgreSQL for analytics data retrieval.
- Built the application using Python and aiogram.



### [NutriBot](https://github.com/MrGrose/NutriBot)
*Local RAG assistant for document-based question answering.*
- Built a document retrieval pipeline using LangChain and FAISS.
- Processed uploaded documents, generated embeddings, and retrieved relevant context.
- Used local language models through Ollama to generate answers based on retrieved information.

### [Pillstore]()
*E-commerce backend built with FastAPI.*
- Developed backend functionality for an online store, including user authentication, shopping cart, and order management.
- Implemented administrative functionality for managing store operations.
- Integrated Telegram Mini App with the backend.
- Built API endpoints to support storefront functionality and user interactions.

---
### Engineering Focus

I am particularly interested in:
  - Backend architecture and domain-driven business logic.
  - Reliable payment and order processing.
  - Database performance and transaction management.
  - Asynchronous systems and background job processing.
  - API integrations and automation.
  - Practical applications of LLMs and retrieval-augmented generation.

---

## Contacts

- Email: [grachev.backend@gmail.com](mailto:grachev.backend@gmail.com)

