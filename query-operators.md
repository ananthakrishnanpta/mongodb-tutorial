# Query Operators in MongoDB
MongoDB query operators are used to specify conditions in queries. These operators allow you to filter documents based on various criteria.

### Syntax
```javascript
db.collection.find({ field: { <operator>: value } });
```

### Operators Categories
1. **Comparison Operators**
2. **Logical Operators**
3. **Element Operators**
4. **Evaluation Operators**
5. **Array Operators**
6. **Bitwise Operators**

---

## Comparison Operators

### `$eq` (Equal)
Find employees with a salary of 60000:
```javascript
db.employees.find({ salary: { $eq: 60000 } });
```

### `$ne` (Not Equal)
Find employees not in the HR department:
```javascript
db.employees.find({ department: { $ne: "HR" } });
```

### `$gt` (Greater Than)
Find employees with a salary greater than 55000:
```javascript
db.employees.find({ salary: { $gt: 55000 } });
```

### `$gte` (Greater Than or Equal)
Find employees aged 30 or older:
```javascript
db.employees.find({ age: { $gte: 30 } });
```

### `$lt` (Less Than)
Find employees younger than 30:
```javascript
db.employees.find({ age: { $lt: 30 } });
```

### `$lte` (Less Than or Equal)
Find employees with a salary of 50000 or less:
```javascript
db.employees.find({ salary: { $lte: 50000 } });
```

### `$in` (In)
Find employees in the HR or IT department:
```javascript
db.employees.find({ department: { $in: ["HR", "IT"] } });
```

### `$nin` (Not In)
Find employees not in the Finance or Marketing department:
```javascript
db.employees.find({ department: { $nin: ["Finance", "Marketing"] } });
```

---

## Logical Operators

### `$and`
Find employees in the IT department with a salary greater than 60000:
```javascript
db.employees.find({ $and: [{ department: "IT" }, { salary: { $gt: 60000 } }] });
```

### `$or`
Find employees in HR or earning less than 60000:
```javascript
db.employees.find({ $or: [{ department: "HR" }, { salary: { $lt: 60000 } }] });
```

### `$not`
Find employees not in the IT department:
```javascript
db.employees.find({ department: { $not: { $eq: "IT" } } });
```

### `$nor`
Find employees not in HR and not earning more than 60000:
```javascript
db.employees.find({ $nor: [{ department: "HR" }, { salary: { $gt: 60000 } }] });
```

---

## Element Operators

### `$exists`
Find employees with a `bonus` field:
```javascript
db.employees.find({ bonus: { $exists: true } });
```

### `$type`
Find employees with a salary stored as a number:
```javascript
db.employees.find({ salary: { $type: "number" } });
```

---

## Evaluation Operators

### `$regex`
Find employees with names starting with "J":
```javascript
db.employees.find({ name: { $regex: /^J/ } });
```

### `$expr`
Find employees whose salary is greater than their bonus (if bonus exists):
```javascript
db.employees.find({ $expr: { $gt: ["$salary", "$bonus"] } });
```

---

## Array Operators

### `$all`
Find employees with multiple skills (assuming a `skills` array):
```javascript
db.employees.find({ skills: { $all: ["JavaScript", "Python"] } });
```

### `$size`
Find employees with exactly 3 skills:
```javascript
db.employees.find({ skills: { $size: 3 } });
```

### `$elemMatch`
Find employees with a skill level greater than 8 in JavaScript (assuming `skills` is an array of objects):
```javascript
db.employees.find({ skills: { $elemMatch: { name: "JavaScript", level: { $gt: 8 } } } });
```

---

## Bitwise Operators

### `$bitsAllSet`
Find employees with a specific permission flag (e.g., `5`):
```javascript
db.employees.find({ permissions: { $bitsAllSet: 5 } });
```

### `$bitsAnyClear`
Find employees with at least one permission flag unset (e.g., `2`):
```javascript
db.employees.find({ permissions: { $bitsAnyClear: 2 } });
```

---

## Useful Commands for Testing

- **List All Documents**:
  ```javascript
  db.employees.find();
  ```
- **Count Filtered Documents**:
  ```javascript
  db.employees.countDocuments({ department: "IT" });
  ```
- **Sort Results**:
  ```javascript
  db.employees.find().sort({ salary: -1 });
  ```

---

