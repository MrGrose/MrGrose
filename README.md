### Python Backend Developer | FastAPI · Django · PostgreSQL | AI/LLM Integrations

## Обо мне
Разрабатываю backend-системы, API и интеграции для бизнес-приложений. Есть коммерческий опыт разработки CRM-платформы и собственные проекты в e-commerce, B2B и AI/LLM.

В работе уделяю внимание бизнес-логике, надёжности данных, производительности PostgreSQL и качеству архитектуры.

## Основные проекты

### [Shopstore](https://github.com/MrGrose/Shopstore)
**Интернет-магазин спортивного инвентаря · production-проект**

Самостоятельно спроектировал и развиваю backend интернет-магазина. На витрине около **13 000 товаров**, в базе данных — около **17 000 записей о товарах**. В проект входят каталог, заказы, оплата по СБП, Telegram Mini App, операторская админка и интеграции с внешними сервисами.

- Разделил жизненные циклы заказа, оплаты и поставки: их статусы управляются независимо.
- Реализовал оплату по СБП: QR-код с ограниченным сроком действия, несколько попыток оплаты, идемпотентная обработка callback и сверка статусов с платёжным шлюзом.
- Внедрил **transactional outbox** для Telegram-уведомлений: событие сохраняется в PostgreSQL вместе с бизнес-операцией, а отдельный worker доставляет его с помощью `FOR UPDATE SKIP LOCKED` и повторных попыток.
- Реализовал конкурентный импорт каталога поставщика: атомарный захват товара в PostgreSQL и Redis-lock защищают от повторной обработки одного SKU разными worker-процессами.
- Настроил версионирование Redis-кэша через `INCR` и fallback на PostgreSQL при недоступности Redis.
- Разработал операторскую админку с отдельными очередями проверки наличия, сборки заказов и отслеживания доставки.
- Подготовил Docker Compose-инфраструктуру, health/readiness-проверки, резервное копирование PostgreSQL и CI на GitHub Actions.
- Использовал Blue/Green Deployment для обновления приложения; организовал хранение и раздачу медиа через SeaweedFS с CDN-кешированием.
- Тестовая база включает более **200 файлов pytest** с unit-, integration- и e2e-сценариями.

**Стек:** Python, FastAPI, SQLAlchemy (async), PostgreSQL, Alembic, Redis, RQ, Pydantic, aiogram, aiohttp, Playwright, Docker Compose, GitHub Actions, pytest.

### [B2B-Commerce](https://github.com/MrGrose/B2B-Commerce)
**Платформа оптовой торговли для компаний**

Самостоятельно разработал B2B-платформу: компании-клиенты, каталог товаров, корзина, счета, складские остатки, резервы и финансовые операции. Backend на FastAPI с доменными модулями: auth, catalog, inventory, cart, invoices, finance, payments. Одна PostgreSQL и общий деплой, фоновые задачи в ARQ worker. Административный интерфейс и личный кабинет используют ту же бизнес-логику, что и JSON API.

- Разделил приложение на доменные модули: компании, каталог, корзина, счета, склад, финансы, платежи, авторизация и аудит.
- Реализовал конкурентное создание счетов с PostgreSQL row-level locking (`SELECT FOR UPDATE`) и фиксированным порядком блокировок для защиты от deadlock.
- Организовал резервирование товара при выставлении счёта: корзина не меняет складские остатки, просроченный счёт освобождает резерв, а фактическое списание происходит при отгрузке.
- Добавил идемпотентное подтверждение оплаты через `Idempotency-Key`.
- Реализовал журнал складских движений и финансовые отчёты на основе снимков цен и реквизитов на момент выставления счёта.
- Настроил server-side sessions, Argon2id, httpOnly cookies, CSRF-защиту и rate limit с fail-closed поведением при недоступности Redis.
- Вынес периодические операции в фоновые задачи ARQ.
- Настроил CI: Ruff, pytest, проверка Alembic, сборка Docker-образа и публикация в GHCR.
- Подготовил **45 pytest-модулей** для проверки счетов, резервирования, авторизации и безопасности.

**Стек:** Python, FastAPI, SQLAlchemy (async), PostgreSQL, Alembic, Redis, ARQ, Argon2id, Jinja2, HTMX, Docker Compose, GitHub Actions, pytest.

### [RAG Platform](https://github.com/MrGrose/rag-platform)
**Мультитенантный сервис поиска по документам**

Backend RAG-сервиса для ответов на вопросы по документам с проверяемыми ссылками на источники. Сервис объединяет загрузку и индексацию документов, векторный и полнотекстовый поиск, ранжирование фрагментов и генерацию ответа языковой моделью.

- Реализовал обработку документов: извлечение текста из PDF и других форматов, chunking, генерация embeddings и индексация.
- Организовал гибридный поиск на PostgreSQL: `pgvector` для векторного поиска и полнотекстовый поиск для лексического совпадения.
- Добавил объединение результатов через score fusion и этап reranking.
- Реализовал проверку цитат, чтобы ссылки в ответах соответствовали найденным фрагментам документов.
- Разделил данные по организациям и базам знаний, добавил API-ключи на уровне организации.
- Ограничил конкуренцию и бюджет LLM-запросов на чат через Redis.
- Вынес фоновую индексацию в ARQ и transactional outbox.
- Добавил асинхронные evaluation-прогоны на датасетах для оценки качества поиска.
- Разделил приложение на domain, application, infrastructure и API; предусмотрел сменные адаптеры embeddings и файловых хранилищ, включая Ollama и S3/MinIO.

**Стек:** Python, FastAPI, PostgreSQL, pgvector, полнотекстовый поиск, Redis, ARQ, embeddings, reranking, LLM API, Ollama, S3/MinIO.

## Другие проекты

### [Eventflow](https://github.com/MrGrose/eventflow) — событийный backend обработки заказов

Инженерный проект для изучения и реализации надёжной событийной архитектуры. В нём реализованы transactional outbox, отдельный publisher worker, переключение между RabbitMQ и Kafka через конфигурацию, retry, DLQ, ручное подтверждение ACK/commit и идемпотентные consumers. Используется семантика at-least-once с явной обработкой повторной доставки. Для наблюдаемости подключены Prometheus и Grafana.

### [ERP-OMS-WMS](https://github.com/MrGrose/ERP-OMS-WWS) — backend системы управления заказами и складом

Backend MVP, объединяющий функциональность ERP, OMS и WMS. Backend MVP на FastAPI разделён на **14 доменных областей**. Inventory — единственный компонент, который изменяет `on_hand` и `reserved`; остальные домены проводят складские операции через его сервисы.

Реализованы жизненный цикл заказа, конкурентное резервирование, идемпотентная обработка платёжных webhook, частичные отгрузки, закупки, приёмка товаров, межскладские перемещения, возвраты, отчётность и аудит. По документации проекта — **7 миграций Alembic и 28 тестов**: 22 запускаются по умолчанию и 6 предназначены для PostgreSQL integration.

Это MVP backend-системы, а не production-hardened продукт.

### [PillStore](https://github.com/MrGrose/Pillstore) — интернет-магазин на FastAPI

Самостоятельный e-commerce-проект с ролями покупателей и продавцов, каталогом с русско- и англоязычным поиском, фильтрами, корзиной, заказами и административным интерфейсом. Есть сбор данных о товарах, автоматический перевод и интеграция с Telegram, включая привязку аккаунта и Mini App.

**Стек:** Python 3.12, FastAPI, SQLAlchemy 2, PostgreSQL, Alembic, Pydantic, JWT, Playwright, BeautifulSoup, Jinja2, Docker, Poetry, aiogram, aiohttp.

### Небольшие проекты и эксперименты

- [Video Analytics Bot](https://github.com/MrGrose/video-analytics-bot) — Telegram-бот, который преобразует вопросы на естественном языке в SQL-запросы с помощью LLM и получает аналитические данные из PostgreSQL.
- [NutriBot](https://github.com/MrGrose/NutriBot) — локальный RAG-ассистент для работы с документами на LangChain, FAISS, embeddings и Ollama.

## Технологии

- **Backend:** Python, FastAPI, Django, Django REST Framework, SQLAlchemy, Pydantic, asyncio
- **Базы данных и поиск:** PostgreSQL, Redis, pgvector, Qdrant, FAISS
- **Фоновые задачи:** RQ, ARQ, async workers, scheduled jobs
- **Интеграции:** REST API, HTTPX, aiohttp, Playwright, aiogram
- **AI/LLM:** RAG, embeddings, LangChain, LiteLLM, DeepSeek, OpenRouter, Ollama
- **Инфраструктура:** Docker, Docker Compose, Linux, Nginx, GitHub Actions, GitLab CI/CD
- **Качество и инструменты:** pytest, Alembic, Ruff, mypy, OpenAPI, Git

## Инженерные интересы

- Архитектура backend-приложений и доменная бизнес-логика
- Транзакции PostgreSQL, блокировки и конкурентный доступ к данным
- Идемпотентность, transactional outbox и надёжная фоновая обработка
- Производительность SQL-запросов и проектирование схем данных
- Интеграции с внешними API и автоматизация бизнес-процессов
- Практическое применение LLM, RAG, гибридного поиска и reranking

---

<a href="mailto:grachev.backend@gmail.com">grachev.backend@gmail.com</a>



