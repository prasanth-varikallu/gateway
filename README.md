# API Gateway

The **API Gateway** is the single entry point for all external requests in the Retail Management microservices demo. It provides intelligent routing and cross-cutting concerns like distributed tracing for the entire system.

## Features
- **Centralized Routing**: Directs traffic to the Catalog, Order, and Inventory services based on URL patterns.
- **Service Decoupling**: Clients interact with a single endpoint, hiding the internal microservice architecture.
- **Request Filtering**: Automatically strips prefixes (e.g., `/catalog/**` becomes `/**` for the backend) for seamless routing.
- **Observability**: Acts as the first point of trace generation in the Zipkin-based distributed tracing system.

## Routing Table
| Path | Target Service |
| :--- | :--- |
| `/catalog/**` | `http://catalog:8080` |
| `/order/**` | `http://order:8080` |
| `/inventory/**` | `http://inventory:8080` |

## Tech Stack
- **Java 25**
- **Spring Boot 3.5.x**
- **Spring Cloud Gateway**
- **Micrometer Tracing + Zipkin**

## Configuration
- **Port**: 8081
- **Zipkin**: `http://zipkin:9411/api/v2/spans`

## Running the Service

### Prerequisites
- Java 25
- Maven
- Back-end services running (Catalog, Order, Inventory)

### Locally
```bash
./mvnw spring-boot:run
```

### Docker
```bash
docker build -t gateway .
docker run -p 8081:8081 gateway
```
