# MongoDB Example: Library Database

## Step 1: Create the `library` Database

To create and use the `library` database:
```javascript
use library
```

---

## Step 2: Create a `books` Collection

Insert sample data into the `books` collection:
```javascript
db.books.insertMany([
  {
    title: "To Kill a Mockingbird",
    author: "Harper Lee",
    genre: "Fiction",
    publishedYear: 1960,
    copiesAvailable: 5
  },
  {
    title: "1984",
    author: "George Orwell",
    genre: "Dystopian",
    publishedYear: 1949,
    copiesAvailable: 2
  },
  {
    title: "The Great Gatsby",
    author: "F. Scott Fitzgerald",
    genre: "Classic",
    publishedYear: 1925,
    copiesAvailable: 3
  },
  {
    title: "The Catcher in the Rye",
    author: "J.D. Salinger",
    genre: "Classic",
    publishedYear: 1951,
    copiesAvailable: 4
  }
]);
```

---

## Step 3: Query the `books` Collection

### 3.1 List All Books
Retrieve all documents from the `books` collection:
```javascript
db.books.find();
```

### 3.2 Find Books by Genre
Retrieve all books in the "Classic" genre:
```javascript
db.books.find({ genre: "Classic" });
```

### 3.3 Find Books Published After a Certain Year
Retrieve books published after 1950:
```javascript
db.books.find({ publishedYear: { $gt: 1950 } });
```

---

## Step 4: Update Documents

### 4.1 Update the Number of Copies Available
Increase the number of copies for "1984" by 3:
```javascript
db.books.updateOne(
  { title: "1984" },
  { $inc: { copiesAvailable: 3 } }
);
```

### 4.2 Add a New Field
Add a `rating` field to "To Kill a Mockingbird":
```javascript
db.books.updateOne(
  { title: "To Kill a Mockingbird" },
  { $set: { rating: 4.8 } }
);
```

---

## Step 5: Delete Documents

### 5.1 Remove a Specific Book
Remove "The Catcher in the Rye":
```javascript
db.books.deleteOne({ title: "The Catcher in the Rye" });
```

### 5.2 Remove All Books of a Specific Genre
Remove all "Dystopian" books:
```javascript
db.books.deleteMany({ genre: "Dystopian" });
```

---

## Step 6: Aggregation

### 6.1 Count Books by Genre
Count the number of books in each genre:
```javascript
db.books.aggregate([
  { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
]);
```

### 6.2 Find Average Published Year
Find the average year of publication:
```javascript
db.books.aggregate([
  { $group: { _id: null, averageYear: { $avg: "$publishedYear" } } }
]);
```

---

## Step 7: Indexing

### 7.1 Create an Index
Create an index on the `title` field for faster searching:
```javascript
db.books.createIndex({ title: 1 });
```

### 7.2 List Indexes
List all indexes in the `books` collection:
```javascript
db.books.getIndexes();
```

---

## Step 8: Backup and Restore

### 8.1 Export the `books` Collection
Export the collection to a JSON file:
```bash
mongoexport --db=library --collection=books --out=books.json
```

### 8.2 Import the `books` Collection
Import the collection from a JSON file:
```bash
mongoimport --db=library --collection=books --file=books.json
```

---

## Step 9: Advanced Queries

### 9.1 Books with Multiple Conditions
Find books published before 1960 and with more than 3 copies available:
```javascript
db.books.find({
  $and: [
    { publishedYear: { $lt: 1960 } },
    { copiesAvailable: { $gt: 3 } }
  ]
});
```

### 9.2 Regex Query
Find books whose title contains "The":
```javascript
db.books.find({ title: { $regex: /The/ } });
```
