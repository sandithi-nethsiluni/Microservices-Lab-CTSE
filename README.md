# Microservices Lab - SE4010

A complete microservices system with **Item Service**, **Order Service**, **Payment Service**, and **API Gateway**.

## Architecture

```
Client (Postman / Browser)
         ↓
    API Gateway :8080
    /items | /orders | /payments
         ↓
Item :8081 | Order :8082 | Payment :8083
```

## Technology Stack

| Service        | Technology   | Port |
|----------------|--------------|------|
| Item Service   | Node.js + Express | 8081 |
| Order Service  | Spring Boot  | 8082 |
| Payment Service| Spring Boot  | 8083 |
| API Gateway    | Spring Cloud Gateway | 8080 |

## Prerequisites

- Docker & Docker Compose
- Maven (for local build)
- Node.js (optional, for local item-service dev)

## Build & Run

### 1. Build Spring Boot services (required before Docker build)

```bash
cd order-service && mvn clean package -DskipTests && cd ..
cd payment-service && mvn clean package -DskipTests && cd ..
cd api-gateway && mvn clean package -DskipTests && cd ..
```

### 2. Start all services with Docker Compose

From the project root:

```bash
docker-compose build
docker-compose up
```

Or run in background:

```bash
docker-compose up -d
```

### 3. Verify

- API Gateway: http://localhost:8080
- Item Service (direct): http://localhost:8081
- Order Service (direct): http://localhost:8082
- Payment Service (direct): http://localhost:8083

## API Endpoints (via Gateway - port 8080)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /items | List all items |
| POST | /items | Create item `{"name": "Headphones"}` |
| GET | /items/{id} | Get item by ID |
| GET | /orders | List all orders |
| POST | /orders | Place order `{"item": "Laptop", "quantity": 2, "customerId": "C001"}` |
| GET | /orders/{id} | Get order by ID |
| GET | /payments | List all payments |
| POST | /payments/process | Process payment `{"orderId": 1, "amount": 1299.99, "method": "CARD"}` |
| GET | /payments/{id} | Get payment by ID |

## Testing with Postman

1. Import `postman_collection.json` into Postman
2. Ensure `docker-compose up` is running
3. Run requests through the API Gateway at `http://localhost:8080`

## Commands

```bash
# View logs
docker-compose logs -f

# Stop all
docker-compose down
```
