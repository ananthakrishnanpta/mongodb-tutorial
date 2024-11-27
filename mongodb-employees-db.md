
# MongoDB `mongosh` `employee` db example


### Start MongoDB Shell


### Create or Select the `employees` Database
```javascript
use employees
```

This switches to the `employees` database or creates it if it doesn’t exist.

---

## Create and Populate Collections

### Insert Employee Data

#### Create `employees` Collection and Add Documents
```javascript
db.employees.insertMany([
    { emp_id: 101, name: "John Doe", age: 30, department: "HR", salary: 60000 },
    { emp_id: 102, name: "Jane Smith", age: 25, department: "Finance", salary: 55000 },
    { emp_id: 103, name: "Sam Wilson", age: 35, department: "IT", salary: 75000 },
    { emp_id: 104, name: "Sara Brown", age: 28, department: "Marketing", salary: 50000 }
]);
```

#### Create `departments` Collection and Add Documents
```javascript
db.departments.insertMany([
    { dept_id: 1, name: "HR", manager: "John Doe" },
    { dept_id: 2, name: "Finance", manager: "Jane Smith" },
    { dept_id: 3, name: "IT", manager: "Sam Wilson" },
    { dept_id: 4, name: "Marketing", manager: "Sara Brown" }
]);
```

---

## Querying Data

### Retrieve All Documents
Fetch all employees:
```javascript
db.employees.find();
```

### Filter by Conditions
Find employees in the IT department:
```javascript
db.employees.find({ department: "IT" });
```

### Retrieve Specific Fields
Fetch only names and salaries:
```javascript
db.employees.find({}, { name: 1, salary: 1, _id: 0 });
```

### Count Documents
Count the number of employees:
```javascript
db.employees.countDocuments();
```

### Aggregate Data
Find the average salary in each department:
```javascript
db.employees.aggregate([
    { $group: { _id: "$department", avgSalary: { $avg: "$salary" } } }
]);
```

---

## Updating Data

### Update a Single Document
Increase John Doe's salary by 10%:
```javascript
db.employees.updateOne(
    { name: "John Doe" },
    { $mul: { salary: 1.1 } }
);
```

### Update Multiple Documents
Add a `bonus` field with a default value of `5000` to all employees:
```javascript
db.employees.updateMany({}, { $set: { bonus: 5000 } });
```

---

## Deleting Data

### Delete a Single Document
Remove the employee with `emp_id: 104`:
```javascript
db.employees.deleteOne({ emp_id: 104 });
```

### Delete Multiple Documents
Remove all employees with a salary less than `55000`:
```javascript
db.employees.deleteMany({ salary: { $lt: 55000 } });
```

---

## Advanced Operations

### Join Collections
Fetch employee details along with their department manager:
```javascript
db.employees.aggregate([
    {
        $lookup: {
            from: "departments",
            localField: "department",
            foreignField: "name",
            as: "departmentDetails"
        }
    }
]);
```

### Indexing
Create an index on the `emp_id` field for faster queries:
```javascript
db.employees.createIndex({ emp_id: 1 });
```

### Backup and Restore
Backup the `employees` database:
```bash
mongodump --db=employees --out=/path/to/backup
```
Restore the `employees` database:
```bash
mongorestore --db=employees /path/to/backup/employees
```

---

## Dropping a Collection or Database

### Drop the `employees` Collection
```javascript
db.employees.drop();
```

### Drop the Entire `employees` Database
```javascript
db.dropDatabase();
```

---

## Useful Commands

- **List All Databases**:
  ```javascript
  show dbs;
  ```
- **List All Collections in the Current Database**:
  ```javascript
  show collections;
  ```

---
