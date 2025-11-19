---
name: backend-languages
description: Backend programming languages including Node.js, Python, Java, Go, PHP, Rust, C++, and ASP.NET Core. Master server-side development, APIs, databases, and enterprise systems.
---

# Backend Languages & Development

## Quick Start

Backend development involves building server-side applications that power web services, APIs, and enterprise systems. Multiple languages excel at different tasks:

- **Node.js/JavaScript** - JavaScript on server, async/event-driven
- **Python** - Elegant syntax, great for data and web
- **Java** - Enterprise scale, performance, mature ecosystem
- **Go** - Compiled, fast, great for microservices
- **PHP** - Web-focused, easy deployment
- **Rust** - Memory-safe, performance-critical systems
- **C++** - Systems programming, maximum performance

## Node.js Backend

```javascript
// Express Server
const express = require('express');
const app = express();

// Middleware
app.use(express.json());

// Database Setup with Prisma
const { PrismaClient } = require('@prisma/client');
const prisma = new PrismaClient();

// Routes
app.get('/api/users', async (req, res) => {
  try {
    const users = await prisma.user.findMany();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.post('/api/users', async (req, res) => {
  const user = await prisma.user.create({
    data: { name: req.body.name, email: req.body.email }
  });
  res.status(201).json(user);
});

// Error Handling
app.use((err, req, res, next) => {
  console.error(err);
  res.status(500).json({ error: 'Internal Server Error' });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

## Python Backend

```python
# Django Web Framework
from django.urls import path
from django.http import JsonResponse
from django.views.decorators.http import require_http_methods
from .models import User

@require_http_methods(["GET"])
def get_users(request):
    users = User.objects.all().values()
    return JsonResponse(list(users), safe=False)

@require_http_methods(["POST"])
def create_user(request):
    import json
    data = json.loads(request.body)
    user = User.objects.create(name=data['name'], email=data['email'])
    return JsonResponse({'id': user.id, 'name': user.name})

# FastAPI Alternative (Modern)
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    email: str

@app.get("/users")
async def list_users():
    users = await User.objects.all()
    return users

@app.post("/users")
async def create_user(user: User):
    new_user = await User.objects.create(**user.dict())
    return new_user
```

## Java Backend

```java
// Spring Boot Application
package com.example.api;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

// Entity
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Getters and setters...
}

// Repository
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByEmail(String email);
}

// Controller
@RestController
@RequestMapping("/api/users")
public class UserController {
    @Autowired
    private UserRepository userRepository;

    @GetMapping
    public List<User> getUsers() {
        return userRepository.findAll();
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
}
```

## Go Backend

```go
package main

import (
    "encoding/json"
    "net/http"
    "github.com/gorilla/mux"
    "gorm.io/gorm"
    "gorm.io/driver/postgres"
)

// User Model
type User struct {
    ID    uint   `json:"id"`
    Name  string `json:"name"`
    Email string `json:"email"`
}

// Database Setup
var db *gorm.DB

func init() {
    var err error
    db, err = gorm.Open(postgres.Open(dsn), &gorm.Config{})
    if err != nil {
        panic("Failed to connect to database")
    }
}

// Get Users Handler
func GetUsers(w http.ResponseWriter, r *http.Request) {
    var users []User
    db.Find(&users)

    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(users)
}

// Create User Handler
func CreateUser(w http.ResponseWriter, r *http.Request) {
    var user User
    json.NewDecoder(r.Body).Decode(&user)

    result := db.Create(&user)
    if result.Error != nil {
        http.Error(w, result.Error.Error(), 500)
        return
    }

    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(http.StatusCreated)
    json.NewEncoder(w).Encode(user)
}

// Main
func main() {
    router := mux.NewRouter()
    router.HandleFunc("/api/users", GetUsers).Methods("GET")
    router.HandleFunc("/api/users", CreateUser).Methods("POST")

    http.ListenAndServe(":3000", router)
}
```

## Rust Systems Programming

```rust
use actix_web::{web, App, HttpServer, HttpResponse};
use sqlx::PgPool;
use serde::{Deserialize, Serialize};

#[derive(Serialize, Deserialize)]
struct User {
    id: i32,
    name: String,
    email: String,
}

// Get Users Handler
async fn get_users(pool: web::Data<PgPool>) -> HttpResponse {
    match sqlx::query_as::<_, User>(
        "SELECT id, name, email FROM users"
    )
    .fetch_all(pool.get_ref())
    .await {
        Ok(users) => HttpResponse::Ok().json(users),
        Err(_) => HttpResponse::InternalServerError().finish(),
    }
}

// Create User Handler
async fn create_user(
    pool: web::Data<PgPool>,
    user: web::Json<User>
) -> HttpResponse {
    match sqlx::query(
        "INSERT INTO users (name, email) VALUES ($1, $2)"
    )
    .bind(&user.name)
    .bind(&user.email)
    .execute(pool.get_ref())
    .await {
        Ok(_) => HttpResponse::Created().json(user),
        Err(_) => HttpResponse::InternalServerError().finish(),
    }
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    let pool = PgPool::connect("postgres://localhost/mydb").await.unwrap();

    HttpServer::new(move || {
        App::new()
            .app_data(web::Data::new(pool.clone()))
            .route("/api/users", web::get().to(get_users))
            .route("/api/users", web::post().to(create_user))
    })
    .bind("127.0.0.1:3000")?
    .run()
    .await
}
```

## Core Backend Concepts

### RESTful API Design
- **GET** - Retrieve resources
- **POST** - Create resources
- **PUT/PATCH** - Update resources
- **DELETE** - Remove resources
- **Status Codes** - 2xx (success), 4xx (client error), 5xx (server error)

### Authentication & Security
- **JWT** - JSON Web Tokens for stateless auth
- **OAuth 2.0** - Third-party authentication
- **Password Hashing** - bcrypt, Argon2
- **HTTPS/TLS** - Encrypted communication
- **SQL Injection Prevention** - Parameterized queries
- **CORS** - Cross-Origin Resource Sharing

### Database Integration
- **SQL** - PostgreSQL, MySQL
- **NoSQL** - MongoDB, Redis
- **ORM** - Object-Relational Mapping (Sequelize, SQLAlchemy, Hibernate)
- **Transactions** - ACID compliance
- **Connection Pooling** - Efficient resource management

### Error Handling

```javascript
// Express error handling
app.use((err, req, res, next) => {
  const status = err.status || 500;
  const message = err.message || 'Internal Server Error';

  res.status(status).json({
    error: {
      status,
      message,
      timestamp: new Date().toISOString()
    }
  });
});
```

### Testing Backends

```javascript
// Jest Testing
describe('User API', () => {
  test('GET /api/users returns all users', async () => {
    const res = await request(app).get('/api/users');
    expect(res.status).toBe(200);
    expect(Array.isArray(res.body)).toBe(true);
  });

  test('POST /api/users creates new user', async () => {
    const newUser = { name: 'John', email: 'john@example.com' };
    const res = await request(app)
      .post('/api/users')
      .send(newUser);
    expect(res.status).toBe(201);
    expect(res.body.id).toBeDefined();
  });
});
```

## Language Comparison

| Language | Use Case | Learning Curve | Performance | Ecosystem | Scalability |
|----------|----------|-----------------|-------------|-----------|-------------|
| Node.js | Real-time, APIs | Easy | Good | Huge | Good |
| Python | Web, Data, AI | Easy | Medium | Good | Good |
| Java | Enterprise | Hard | Excellent | Excellent | Excellent |
| Go | Microservices | Medium | Excellent | Growing | Excellent |
| PHP | Web apps | Easy | Good | Large | Good |
| Rust | Systems | Hard | Excellent | Growing | Excellent |

## Best Practices

- Use async/await for non-blocking operations
- Implement proper error handling and logging
- Use databases efficiently (indexing, query optimization)
- Secure your APIs (authentication, validation)
- Write comprehensive tests
- Document your APIs (Swagger/OpenAPI)
- Monitor and log for debugging
- Use containerization (Docker)
- Version your APIs

## Resources

- [Node.js Docs](https://nodejs.org/docs)
- [Python Docs](https://docs.python.org)
- [Java Spring Boot](https://spring.io/projects/spring-boot)
- [Go Official Docs](https://golang.org/doc)
- [Rust Programming](https://www.rust-lang.org/learn)

## Related Skills

- **Databases** - SQL and NoSQL design
- **APIs** - RESTful and GraphQL design
- **DevOps** - Docker, Kubernetes, deployment
- **Testing** - Unit and integration tests
- **Cloud Platforms** - AWS, GCP, Azure
