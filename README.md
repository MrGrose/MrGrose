# Python Backend Developer

FastAPI · PostgreSQL · Redis · AI/LLM

Проектирую backend для e-commerce, B2B и RAG-сервисов: каталог и заказы, оплата, фоновые задачи, интеграции и поиск по документам. Внимание к бизнес-логике, транзакциям, идемпотентности и качеству данных.

## Проекты

### [Shopstore](https://github.com/MrGrose/shopstore)

GitHub: https://github.com/MrGrose/shopstore

Интернет-магазин спортивного инвентаря, production-проект.

- 19,4 тыс. товарных карточек, 109 тыс. вариантов, 12,7 тыс. товаров в наличии, 88,8 тыс. изображений и 23 ГБ медиа.
- Оплата по СБП: QR на 15 минут, до 5 попыток, идемпотентная обработка callback и сверка статусов с платежным шлюзом.
- Transactional outbox для Telegram: 1994 успешные доставки из 2011 событий, среднее время около 32 секунд.
- Конкурентный импорт каталога: атомарный claim SKU в PostgreSQL и Redis-lock. Около 19 тыс. SKU за 30 минут, 15 успешных ночных циклов.
- 15 Docker Compose сервисов, 8 RQ workers, Blue/Green, health/readiness, бэкапы PostgreSQL, 66 миграций Alembic и более 200 файлов pytest.

**Стек:** Python, FastAPI, SQLAlchemy async, PostgreSQL, Alembic, Redis, RQ, aiogram, Playwright, Docker, GitHub Actions.

### [B2B-Commerce](https://github.com/MrGrose/B2B-Commerce)

GitHub: https://github.com/MrGrose/B2B-Commerce

Платформа оптовой торговли: компании, каталог, счета, склад и финансы.

- Backend на FastAPI с доменными модулями: auth, catalog, inventory, cart, invoices, finance, payments. Одна PostgreSQL и общий деплой, фоновые задачи в ARQ worker.
- Конкурентное создание счетов с `SELECT FOR UPDATE` и фиксированным порядком блокировок.
- Резерв при выставлении счета, освобождение при просрочке и списание при отгрузке через журнал складских движений.
- Идемпотентное подтверждение оплаты, Argon2id, server-side sessions, CSRF и rate limit с fail-closed поведением.
- 45 pytest-модулей, 5 контейнеров, сборка Docker-образа и публикация в GHCR.

**Стек:** Python, FastAPI, SQLAlchemy async, PostgreSQL, Alembic, Redis, ARQ, Jinja2, HTMX, Docker, GitHub Actions.

### [RAG Platform](https://github.com/MrGrose/rag-platform)

GitHub: https://github.com/MrGrose/rag-platform

Мультитенантный сервис поиска по документам с проверяемыми цитатами.

- Загрузка PDF и других форматов, chunking, embeddings и индексация в PostgreSQL с pgvector.
- Гибридный поиск: векторный и полнотекстовый, score fusion и reranking.
- Проверка цитат и изоляция данных по организациям и базам знаний.
- Evaluation на 44 вопросах: hit@5 1.00 на синтетическом наборе, отдельный отчет с задержкой и стоимостью.
- Сменные адаптеры embeddings, reranker и LLM, ARQ и transactional outbox.

**Стек:** Python, FastAPI, PostgreSQL, pgvector, Redis, ARQ, embeddings, reranking, LLM API, S3.

## Еще проекты

### [Eventflow](https://github.com/MrGrose/eventflow)

GitHub: https://github.com/MrGrose/eventflow

Событийный backend: transactional outbox, RabbitMQ и Kafka, retry, DLQ, идемпотентные consumers, 72 теста на живых брокерах.

### [ERP-OMS-WWS](https://github.com/MrGrose/ERP-OMS-WWS)

GitHub: https://github.com/MrGrose/ERP-OMS-WWS

Backend ERP/OMS/WMS MVP: 14 доменных областей, заказы, резервы, отгрузки, закупки, возвраты, 28 тестов и 7 миграций.

### [Autohub](https://github.com/MrGrose/autohub)

GitHub: https://github.com/MrGrose/autohub

Каталог автомобилей: Next.js, FastAPI, PostgreSQL, админка, Docker Compose, тесты и CI.

## Технологии

- **Backend:** Python, FastAPI, Django, SQLAlchemy, Pydantic, asyncio
- **Данные:** PostgreSQL, Redis, pgvector, Qdrant, FAISS
- **Фоновые задачи:** RQ, ARQ, async workers
- **Интеграции:** REST, HTTPX, aiohttp, Playwright, aiogram
- **AI/LLM:** RAG, embeddings, reranking, LangChain, DeepSeek, Ollama
- **Инфраструктура:** Docker Compose, Linux, Nginx, GitHub Actions

## Инженерные интересы

- Архитектура backend и доменная бизнес-логика
- Транзакции PostgreSQL, блокировки и конкурентный доступ
- Идемпотентность, transactional outbox и надежная фоновая обработка
- Производительность SQL и проектирование схем данных
- Практическое применение LLM, RAG и гибридного поиска

## Контакты

<a href="mailto:grachev.backend@gmail.com">grachev.backend@gmail.com</a>
