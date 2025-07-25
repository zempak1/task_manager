# Микросервисное приложение "Task Manager"

## Описание

Данный репозиторий содержит пример микросервисного web-приложения для управления задачами (Task Manager), реализованного на современном Java-стеке с использованием DevOps-практик.

**Ключевые технологии:**  
- Spring Boot, Spring Security, JWT, PostgreSQL
- Quarkus (native-image, GraalVM)
- React (SPA, Redux)
- Docker, Docker Compose, Kubernetes
- GitHub Actions (CI/CD)

---

## Архитектура

```
/
├── auth-service               # Микросервис авторизации (Spring Boot + JWT + PostgreSQL)
├── business-service-spring    # Бизнес-сервис задач (Spring Boot)
├── business-service-quarkus   # Альтернативный бизнес-сервис задач (Quarkus + native image)
├── frontend                   # Клиентское SPA-приложение (React)
├── infra/
│   ├── docker-compose.yml     # Компоновка сервисов для локального запуска
│   └── k8s/                   # Манифесты для Kubernetes
└── .github/
    └── workflows/ci-cd.yml    # CI/CD пайплайн (GitHub Actions)
```

### Взаимодействие сервисов

- **auth-service**:  
  Реализует регистрацию, аутентификацию пользователей, выдачу JWT, управление ролями (USER, ADMIN).
- **business-service-spring / business-service-quarkus**:  
  CRUD API для сущности "Задача" (`Task`), интеграция с auth-service для авторизации пользователей.
- **frontend**:  
  SPA-приложение с формами аутентификации и управления задачами (создание, просмотр, редактирование, удаление).
- **infra**:  
  Среда для контейнеризации и оркестрации всех компонентов.

---

## Быстрый старт (локально)

### 1. Клонируйте репозиторий

```sh
git clone https://github.com/your-org/your-repo.git
cd your-repo
```

### 2. Запуск через Docker Compose

```sh
cd infra
docker-compose up --build
```

- Приложение будет доступно по:
    - **Frontend:** http://localhost:3000
    - **Auth-service:** http://localhost:8081
    - **Business-service-spring:** http://localhost:8082
    - **Business-service-quarkus:** http://localhost:8083

### 3. Сборка и запуск в Kubernetes (minikube)

```sh
cd infra/k8s
kubectl apply -f .
```

---

## Сервисы и API

### Auth-service

- Регистрация/логин пользователя
- JWT-аутентификация
- Роли: USER, ADMIN

Документация Swagger: `http://localhost:8081/swagger-ui.html`

### Business-service (Spring / Quarkus)

- CRUD-операции с задачами:
  - `POST /tasks` — создать задачу
  - `GET /tasks` — список задач
  - `GET /tasks/{id}` — получить задачу
  - `PUT /tasks/{id}` — обновить задачу
  - `DELETE /tasks/{id}` — удалить задачу

Документация Swagger:
- Spring: `http://localhost:8082/swagger-ui.html`
- Quarkus: `http://localhost:8083/q/swagger-ui`

### Frontend

- Авторизация пользователя
- Просмотр и управление списком задач
- Роль-базированное отображение (USER, ADMIN)

---

## CI/CD

- Сборка и тесты сервисов через GitHub Actions
- Линтинг кода и анализ качества (SonarQube, ESLint, Prettier)
- Сборка и публикация Docker-образов
- (Опционально) автодеплой в Kubernetes

---

## Документация

- Описание API: Swagger/OpenAPI (автоматически генерируется каждым сервисом)
- База данных: PostgreSQL (структура — в папке `migrations` или в liquibase/flyway скриптах)
- Примеры запросов — см. Swagger или Postman коллекцию (`docs/postman_collection.json`)

---

## Тестирование

- Unit-тесты и интеграционные тесты для backend-сервисов (JUnit)
- Тесты для frontend (Jest/React Testing Library)
- Покрытие тестами проверяется в пайплайне CI/CD

---

## Авторы и поддержка

- [Ваше имя или команда]
- [Контакты для обратной связи]

---

## License

[MIT](LICENSE)
