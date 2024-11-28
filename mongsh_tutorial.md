
# MongoDB `mongosh` Tutorial 

[Examples](https://github.com/ananthakrishnanpta/mongodb-tutorial/blob/main/mongodb-employees-db.md)

---

## Prerequisites

1. Install **MongoDB** and the `mongosh` CLI from [MongoDB Downloads](https://www.mongodb.com/try/download/shell).
2. Ensure MongoDB is running locally or have the connection string to a remote MongoDB instance.

---

## Getting Started

### Start MongoDB Shell

Run the following command to open the MongoDB Shell:
```bash
mongosh
```

### Select or Create a Database
```javascript
use school
```

This switches to the `school` database or creates it if it doesn’t exist.

---

## Create and Populate the `student` Collection

- Inserting documents creates the collection automatically if it doesn't exist,
- otherwise it can be created using the following command :

```javascript
db.createCollection("posts")
```


### Insert Single Document
```javascript
db.student.insertOne({ name: "Alice", age: 20, marks: 85 });
```

### Insert Multiple Documents
```javascript
db.student.insertMany([
    { name: "Bob", age: 22, marks: 90 },
    { name: "Charlie", age: 21, marks: 75 },
    { name: "Diana", age: 23, marks: 88 }
]);
```

---

## Querying Documents

### Retrieve All Documents
```javascript
db.student.find();
```

### Filter by Condition
Find students with marks greater than 80:
```javascript
db.student.find({ marks: { $gt: 80 } });
```

### Retrieve Specific Fields
Fetch only `name` and `age` fields:
```javascript
db.student.find({}, { name: 1, age: 1, _id: 0 });
```

### Count Documents
Count the total number of documents:
```javascript
db.student.countDocuments();
```

### Limit and Skip Results
Limit the result set to 2 students:
```javascript
db.student.find().limit(2);
```
Skip the first 2 documents:
```javascript
db.student.find().skip(2);
```

---

## Update Operations

### Update a Single Document
Modify Diana's marks to 92:
```javascript
db.student.updateOne({ name: "Diana" }, { $set: { marks: 92 } });
```

### Update Multiple Documents
Add 5 marks to all students:
```javascript
db.student.updateMany({}, { $inc: { marks: 5 } });
```

### Replace a Document
Replace Bob's document entirely:
```javascript
db.student.replaceOne({ name: "Bob" }, { name: "Bob", age: 22, marks: 95 });
```

---

## Delete Operations

### Delete a Single Document
Remove a student named Bob:
```javascript
db.student.deleteOne({ name: "Bob" });
```

### Delete Multiple Documents
Remove students with marks less than 80:
```javascript
db.student.deleteMany({ marks: { $lt: 80 } });
```

---

## Advanced Operations

### Aggregation Framework
Calculate the average marks of all students:
```javascript
db.student.aggregate([
    { $group: { _id: null, averageMarks: { $avg: "$marks" } } }
]);
```

### Sorting
Sort by marks in descending order:
```javascript
db.student.find().sort({ marks: -1 });
```

### Indexing
Create an index on the `name` field for faster queries:
```javascript
db.student.createIndex({ name: 1 });
```

### Backup and Restore
Export the `school` database to a file:
```bash
mongodump --db=school --out=/path/to/backup
```
Restore the database from a backup:
```bash
mongorestore --db=school /path/to/backup/school
```

---

## Dropping a Collection or Database

### Drop a Collection
```javascript
db.student.drop();
```

### Drop a Database
```javascript
db.dropDatabase();
```

---

## Additional Notes

- Use `show dbs` to list all databases.
- Use `show collections` to list all collections in the current database.
- For a full list of shell commands, consult the [MongoDB Documentation](https://www.mongodb.com/docs/manual/reference/method/).

---
