# core-api

Go / Основной сервис в рамках проекта cowriter. Выступает в качестве центрального хаба для всех процессов cowriter.

## Technologies

- Go / uber.Fx / gin / sqlx / zap

- REST / Websocket

- Postgres / Redis

- RabbitMQ (producer)

- Prometheus

### Deployment

```sh
docker build -f dockerfile -t doxanocap/core-api:prod .
docker push doxanocap/core-api:prod
```

### Run locally

```bash
docker run --name infra_psql -p 5432:5432 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=password12345 -e POSTGRES_DB=infra-psql -d postgres:14-alpine

docker run --name=redis -p 6379:6379 --restart=always -d redis:latest

docker run -d --hostname rabbit-mq --name rabbit-mq -p 15672:15672 -p 5672:5672 -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3-management
```

### Operations

- Create new migration:
  ```sh
  migrate create -ext sql -dir api/migrations mg_name
  migrate -path api/migrations -database "postgres://postgres:password12345@localhost:5432/infra-psql?sslmode=disable" up
  ```
