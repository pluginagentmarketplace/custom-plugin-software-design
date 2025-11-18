---
name: system-design
description: System design, scalable architecture, and design patterns. Master distributed systems, microservices, and architecture decisions.
---

# System Design & Architecture

## Quick Start

System design covers building scalable, reliable systems.

### Microservices Architecture
```yaml
Services:
  - User Service: Manages user accounts
    - Technology: Node.js + Express
    - Database: PostgreSQL
    - Cache: Redis
  - Post Service: Handles posts
    - Technology: Python + FastAPI
    - Database: MongoDB
  - Notification Service: Sends notifications
    - Technology: Go
    - Queue: RabbitMQ
  - API Gateway: Routes requests
    - Technology: Kong/Nginx
```

### Scalability Patterns
```
Load Balancer
    ├── App Server 1
    ├── App Server 2
    └── App Server 3
         ↓ (all connect to)
    Cache (Redis)
    Database (PostgreSQL with replicas)
    Message Queue (RabbitMQ)
    CDN (CloudFront)
```

### Database Sharding
```
User Service
├── Shard 1 (IDs 1-1000000) → PostgreSQL-1
├── Shard 2 (IDs 1000001-2000000) → PostgreSQL-2
└── Shard 3 (IDs 2000001-3000000) → PostgreSQL-3
```

## Core Concepts

**Scalability**
- Vertical: More powerful servers
- Horizontal: More servers

**Availability**
- Redundancy
- Failover mechanisms
- Load balancing

**Consistency**
- Strong consistency
- Eventual consistency
- CAP Theorem

**Latency**
- Caching (Redis, CDN)
- Database optimization
- Async processing

## Design Patterns

- **MVC** - Model-View-Controller
- **Microservices** - Independent services
- **Event-Driven** - Event-based communication
- **CQRS** - Command Query Responsibility Segregation
- **API Gateway** - Single entry point
- **Circuit Breaker** - Prevent cascading failures

## Resources

- [System Design Interview](https://www.systemdesigninterview.com)
- [Designing Data-Intensive Applications (Book)](https://dataintensive.net)
- [Architecture Patterns (Book)](https://www.oreilly.com/library/view/microservices-patterns/9781617294549)
