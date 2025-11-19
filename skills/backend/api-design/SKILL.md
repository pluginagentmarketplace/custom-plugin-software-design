---
name: api-design
description: API design including REST, GraphQL, and gRPC. Master API architecture, documentation, versioning, and best practices.
---

# API Design & Development

## Quick Start

APIs enable communication between systems.

### RESTful API
```javascript
// Express API
app.get('/api/users/:id', (req, res) => {
  const user = getUserById(req.params.id);
  res.json(user);  // 200 OK
});

app.post('/api/users', (req, res) => {
  const user = createUser(req.body);
  res.status(201).json(user);  // 201 Created
});

app.put('/api/users/:id', (req, res) => {
  const user = updateUser(req.params.id, req.body);
  res.json(user);
});

app.delete('/api/users/:id', (req, res) => {
  deleteUser(req.params.id);
  res.status(204).send();  // 204 No Content
});
```

### GraphQL
```javascript
// GraphQL Schema
const typeDefs = `
  type User {
    id: ID!
    name: String!
    email: String!
    posts: [Post]
  }
  
  type Post {
    id: ID!
    title: String!
    content: String!
    author: User!
  }
  
  type Query {
    user(id: ID!): User
    users: [User]
    post(id: ID!): Post
  }
`;

const resolvers = {
  Query: {
    user: (_, { id }) => User.findById(id),
    users: () => User.findAll(),
    post: (_, { id }) => Post.findById(id)
  },
  User: {
    posts: (user) => Post.findByUserId(user.id)
  }
};
```

## API Best Practices

**Versioning**
- /api/v1/users
- /api/v2/users

**Error Handling**
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "fields": {
      "email": "Must be valid email"
    }
  }
}
```

**Authentication**
- JWT (JSON Web Tokens)
- OAuth 2.0
- API Keys

**Rate Limiting**
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1234567890
```

## Documentation

Use OpenAPI/Swagger:
```yaml
openapi: 3.0.0
info:
  title: User API
  version: 1.0.0
paths:
  /api/users:
    get:
      summary: List all users
      responses:
        200:
          description: Array of users
```

## Resources

- [REST API Best Practices](https://restfulapi.net)
- [GraphQL Official Docs](https://graphql.org)
- [OpenAPI Specification](https://spec.openapis.org)
