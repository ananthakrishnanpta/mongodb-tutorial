---

# MongoDB Tutorial with PowerShell and Atlas Integration

## Table of Contents
1. [Introduction](#introduction)
2. [NoSQL Basics and Types](#nosql-basics-and-types)
3. [Setting Up MongoDB Atlas](#setting-up-mongodb-atlas)
4. [Configuring a Persistent Connection](#configuring-a-persistent-connection)
5. [MongoDB Basics](#mongodb-basics)
   - [Create Database and Collections](#create-database-and-collections)
   - [CRUD Operations](#crud-operations)
6. [Advanced MongoDB Concepts](#advanced-mongodb-concepts)
   - [Aggregation Framework](#aggregation-framework)
   - [Replication](#replication)
   - [Sharding](#sharding)
7. [Real-World Examples of NoSQL Use Cases](#real-world-examples-of-nosql-use-cases)
8. [Conclusion](#conclusion)

---

## Introduction

MongoDB is a document-based NoSQL database designed for high scalability, availability, and flexibility. This tutorial covers:
- MongoDB basics using PowerShell commands.
- Advanced features like aggregation, replication, and sharding.
- NoSQL theory and real-world examples.

---

## NoSQL Basics and Types

### What is NoSQL?

NoSQL databases are non-relational and designed for:
- High performance.
- Horizontal scalability.
- Flexible schemas.

### Types of NoSQL Databases

| **Type**          | **Description**                                                                 | **Examples**                  |
|--------------------|---------------------------------------------------------------------------------|--------------------------------|
| Document-based     | Stores data in documents (e.g., JSON).                                         | MongoDB, CouchDB              |
| Key-Value Stores   | Simple key-value pairs for fast lookups.                                       | Redis, DynamoDB               |
| Column-family      | Stores data in columns rather than rows. Ideal for analytical applications.    | Cassandra, HBase              |
| Graph Databases    | Represents data as nodes and relationships.                                   | Neo4j, ArangoDB               |

### Why MongoDB?
MongoDB combines the flexibility of NoSQL with powerful features like:
- Flexible schema design.
- Aggregation framework.
- Support for replication and sharding.

---

## Setting Up MongoDB Atlas

### Step 1: Create an Atlas Account
1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
2. Log in and create a project.

### Step 2: Configure Your Cluster
1. Create a new cluster with the free-tier option.
2. Choose a cloud provider and region.

### Step 3: Database Access
1. Add a database user under **Database Access**.
2. Assign a username and a secure password.

### Step 4: Network Access
1. Whitelist your IP or set it to `0.0.0.0/0` for open access during testing.

### Step 5: Connection String
1. Copy the connection string (e.g., `mongodb+srv://<username>:<password>@cluster0.mongodb.net/test`).

---

## Configuring a Persistent Connection

### Step 1: Store the Connection String in an Environment Variable
```powershell
$env:MONGO_URI = "mongodb+srv://<username>:<password>@cluster0.mongodb.net/test"
```

### Step 2: Create a Default Database Context
1. Open a new file called `.mongorc.js` in your home directory:
   ```powershell
   notepad ~\.mongorc.js
   ```
2. Add the following:
   ```javascript
   const conn = new Mongo($env.MONGO_URI);
   globalThis.db = conn.getDB("your_database_name");
   ```

### Step 3: Test the Persistent Connection
Start `mongosh`, and your default database context (`db`) will be pre-configured.

---

## MongoDB Basics

### Create Database and Collections

#### Create a Database
```powershell
mongosh --eval "use mydatabase"
```

#### Create a Collection
```powershell
mongosh --eval "db.createCollection('mycollection')"
```

---

### CRUD Operations

#### Insert Documents
```powershell
mongosh --eval "db.mycollection.insertOne({name: 'Alice', age: 30, skills: ['PowerShell', 'MongoDB']})"
```

#### Query Documents
Retrieve all documents:
```powershell
mongosh --eval "db.mycollection.find()"
```

Filter documents:
```powershell
mongosh --eval "db.mycollection.find({age: {$gte: 25}})"
```

#### Update Documents
```powershell
mongosh --eval "db.mycollection.updateOne({name: 'Alice'}, {$set: {age: 31}})"
```

#### Delete Documents
```powershell
mongosh --eval "db.mycollection.deleteOne({name: 'Alice'})"
```

---

## Advanced MongoDB Concepts

### Aggregation Framework

Aggregations transform and analyze data using pipelines.

#### Example: Group and Count
```powershell
mongosh --eval "db.mycollection.aggregate([{$group: {_id: '$skills', count: {$sum: 1}}}])"
```

---

### Replication

Replication ensures high availability by duplicating data across multiple nodes.

#### Enable Replication Locally
1. Start a MongoDB server with replication enabled:
   ```powershell
   mongod --replSet "rs0"
   ```
2. Initialize the replica set:
   ```powershell
   mongosh --eval "rs.initiate()"
   ```

---

### Sharding

Sharding distributes data across multiple servers to scale horizontally.

#### Enable Sharding
1. Start a shard server:
   ```powershell
   mongod --shardsvr --dbpath "C:\data\shard1" --port 27018
   ```
2. Add the shard to the cluster:
   ```powershell
   mongosh --eval "sh.addShard('localhost:27018')"
   ```

---

## Real-World Examples of NoSQL Use Cases

### Example 1: Social Media Platforms
- Database: **MongoDB**
- Data: User profiles, posts, and comments.

### Example 2: E-Commerce Applications
- Database: **Redis**
- Data: Caching, shopping cart management.

### Example 3: Financial Systems
- Database: **Cassandra**
- Data: Transaction logs, analytical queries.

---

## Conclusion

This tutorial provides a comprehensive overview of MongoDB's capabilities, from setup to advanced concepts like replication and sharding. It highlights the versatility of MongoDB and its suitability for various real-world use cases.

Feel free to explore further MongoDB documentation or extend this tutorial to fit specific projects.

---
