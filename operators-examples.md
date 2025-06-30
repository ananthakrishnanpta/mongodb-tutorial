````markdown
## **Step 1: Dataset Setup**

### **Database and Collection Creation**

```javascript
// Use or create a database
use companyDB;

// Insert data into the collection
db.employees.insertMany([
    { name: "Alice", age: 25, department: "HR", salary: 50000, skills: ["communication", "recruitment"] },
    { name: "Bob", age: 30, department: "Engineering", salary: 80000, skills: ["javascript", "node.js", "mongoDB"] },
    { name: "Charlie", age: 35, department: "Finance", salary: 75000, skills: ["accounting", "excel"] },
    { name: "Diana", age: 28, department: "HR", salary: 52000, skills: ["training", "employee engagement"] },
    { name: "Eve", age: 29, department: "Engineering", salary: 90000, skills: ["react", "python", "aws"] },
]);
````

---

## **Step 2: Query Operators**

### **Comparison Operators**

```javascript
// Find employees older than 30
db.employees.find({ age: { $gt: 30 } });

// Find employees with a salary less than or equal to 75000
db.employees.find({ salary: { $lte: 75000 } });

// Find employees in HR or Finance departments
db.employees.find({ department: { $in: ["HR", "Finance"] } });

// Find employees not in the Engineering department
db.employees.find({ department: { $nin: ["Engineering"] } });
```

### **Logical Operators**

```javascript
// Find employees in HR and aged below 30
db.employees.find({ $and: [{ department: "HR" }, { age: { $lt: 30 } }] });

// Find employees aged above 35 or earning above 85000
db.employees.find({ $or: [{ age: { $gt: 35 } }, { salary: { $gt: 85000 } }] });

// Find employees not in the HR department
db.employees.find({ department: { $not: { $eq: "HR" } } });
```

### **Element Operators**

```javascript
// Find employees with a skills field
db.employees.find({ skills: { $exists: true } });

// Find employees whose salary is a double type
db.employees.find({ salary: { $type: "double" } });
```

---

## **Step 3: Array Query Operators**

```javascript
// Find employees with "javascript" in their skills
db.employees.find({ skills: { $all: ["javascript"] } });

// Find employees with at least one skill in ["node.js", "aws"]
db.employees.find({ skills: { $in: ["node.js", "aws"] } });

// Find employees with more than 2 skills
db.employees.find({ skills: { $size: { $gt: 2 } } });

// Find employees where one skill is "python"
db.employees.find({ skills: { $elemMatch: { $eq: "python" } } });
```

---

## **Step 4: Projection Operators**

```javascript
// Include only name and department fields
db.employees.find({}, { name: 1, department: 1 });

// Exclude salary from the results
db.employees.find({}, { salary: 0 });
```

---

## **Step 5: Update Operators**

### **Field Update Operators**

```javascript
// Increase salary by 5000 for Bob
db.employees.updateOne({ name: "Bob" }, { $inc: { salary: 5000 } });

// Set a new field for all employees in HR
db.employees.updateMany({ department: "HR" }, { $set: { bonusEligible: true } });
```

### **Array Update Operators**

```javascript
// Add a new skill to Charlie
db.employees.updateOne({ name: "Charlie" }, { $push: { skills: "data analysis" } });

// Add multiple skills to Diana
db.employees.updateOne({ name: "Diana" }, { $addToSet: { skills: { $each: ["presentation", "time management"] } } });
```

---

## **Step 6: Aggregation Operators**

```javascript
// Group employees by department and calculate average salary
db.employees.aggregate([
    { $group: { _id: "$department", averageSalary: { $avg: "$salary" } } }
]);

// Match employees with salary > 70000 and project their names and salaries
db.employees.aggregate([
    { $match: { salary: { $gt: 70000 } } },
    { $project: { name: 1, salary: 1 } }
]);
```

---

## **Step 7: Full List of Operators with Examples**

| **Category**     | **Operators**                                                                    | **Example**                                                          |
| ---------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **Comparison**   | `$eq`, `$ne`, `$gt`, `$lt`, `$gte`, `$lte`, `$in`, `$nin`                        | `{ salary: { $gt: 70000 } }`                                         |
| **Logical**      | `$and`, `$or`, `$not`, `$nor`                                                    | `{ $and: [{ department: "HR" }, { salary: { $gte: 50000 } }] }`      |
| **Element**      | `$exists`, `$type`                                                               | `{ skills: { $exists: true } }`                                      |
| **Array**        | `$all`, `$elemMatch`, `$size`, `$in`, `$nin`                                     | `{ skills: { $all: ["javascript", "mongoDB"] } }`                    |
| **Projection**   | `$meta`, `$slice`                                                                | `{ skills: { $slice: 2 } }`                                          |
| **Field Update** | `$set`, `$unset`, `$rename`, `$inc`, `$mul`, `$min`, `$max`, `$currentDate`      | `{ $set: { department: "Sales" } }`                                  |
| **Array Update** | `$push`, `$pop`, `$pull`, `$addToSet`, `$each`, `$position`, `$slice`, `$sort`   | `{ $push: { skills: "leadership" } }`                                |
| **Aggregation**  | `$match`, `$group`, `$project`, `$sort`, `$limit`, `$skip`, `$lookup`, `$unwind` | `[ { $group: { _id: "$department", total: { $sum: "$salary" } } } ]` |

---
