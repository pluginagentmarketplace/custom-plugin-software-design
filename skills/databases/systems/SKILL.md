---
name: database-systems
description: Relational and NoSQL databases including PostgreSQL, MongoDB, Redis. Master database design, optimization, and management.
---

# Database Systems & Management

## Quick Start

Databases store and manage application data efficiently.

### PostgreSQL (SQL)
```sql
-- Create Table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Queries
SELECT * FROM users WHERE email = 'john@example.com';
INSERT INTO users (name, email) VALUES ('John', 'john@example.com');
UPDATE users SET name = 'Jane' WHERE id = 1;
DELETE FROM users WHERE id = 1;

-- Joins
SELECT u.name, p.title
FROM users u
JOIN posts p ON u.id = p.user_id;

-- Indexes
CREATE INDEX idx_email ON users(email);
```

### MongoDB (NoSQL)
```javascript
// Insert Document
db.users.insertOne({
    name: "John",
    email: "john@example.com",
    tags: ["developer", "typescript"],
    metadata: { location: "NYC", level: 5 }
});

// Find Documents
db.users.find({ email: "john@example.com" });
db.users.find({ tags: { $in: ["developer"] } });

// Update
db.users.updateOne(
    { email: "john@example.com" },
    { $set: { name: "Jane" } }
);

// Aggregation Pipeline
db.users.aggregate([
    { $match: { tags: "developer" } },
    { $group: { _id: "$level", count: { $sum: 1 } } }
]);
```

### Redis (Cache/Session)
```python
import redis

r = redis.Redis(host='localhost', port=6379)

# Strings
r.set('user:1:name', 'John')
name = r.get('user:1:name')

# Lists
r.lpush('tasks', 'task1', 'task2')
tasks = r.lrange('tasks', 0, -1)

# Sets
r.sadd('tags', 'python', 'javascript')
tags = r.smembers('tags')

# Hashes
r.hset('user:1', 'name', 'John')
r.hset('user:1', 'email', 'john@example.com')
user = r.hgetall('user:1')

# Expiration
r.setex('session:token', 3600, 'abc123')
```

## Database Design

- **Normalization** - Eliminate redundancy (1NF, 2NF, 3NF)
- **Indexes** - Speed up queries
- **Foreign Keys** - Maintain referential integrity
- **Transactions** - ACID compliance
- **Partitioning** - Scale large tables

## Best Practices

- Choose appropriate database type (SQL vs NoSQL)
- Index frequently queried columns
- Monitor query performance
- Regular backups
- Use connection pooling
- Secure credentials
- Plan for scalability
- Document schema

## Resources

- [PostgreSQL Docs](https://www.postgresql.org/docs)
- [MongoDB Docs](https://docs.mongodb.com)
- [Redis Docs](https://redis.io/docs)

## Related Skills

- **SQL** - Query language fundamentals
- **Backend Languages** - Database integration
- **DevOps** - Database backup and replication
