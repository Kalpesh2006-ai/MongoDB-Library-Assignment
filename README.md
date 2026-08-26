# MongoDB and NoSQL – Library Management System

## 1. Introduction

MongoDB is a popular open-source **NoSQL database management system** that stores data in flexible, JSON-like documents instead of traditional rows and columns. MongoDB is designed to handle large amounts of data and can scale easily as applications grow.

Unlike relational databases such as MySQL, MongoDB does not require every record in a collection to have exactly the same structure. This flexibility makes MongoDB useful for modern applications where data structures can change frequently.

In this assignment, a simple **Library Management System** is created using MongoDB. The database contains information about books, authors, and genres. CRUD operations and different search queries are demonstrated using MongoDB commands.

---

# 2. What is NoSQL?

NoSQL means **"Not Only SQL."** NoSQL databases are database systems that do not primarily rely on the traditional relational table-based model.

NoSQL databases can use different data models, including:

* Document databases
* Key-value databases
* Column-family databases
* Graph databases

MongoDB is a **document-oriented NoSQL database**.

### Traditional SQL Database

A relational database generally stores data like:

```text
Students Table

+----+--------+-------+
| ID | Name   | Age   |
+----+--------+-------+
| 1  | Rahul  | 20    |
| 2  | Priya  | 21    |
+----+--------+-------+
```

### MongoDB

MongoDB stores information as documents:

```javascript
{
    name: "Rahul",
    age: 20
}
```

These documents are grouped into collections.

---

# 3. What is MongoDB?

MongoDB is a document-oriented NoSQL database that stores data in **BSON (Binary JSON)** documents.

A MongoDB structure can be represented as:

```text
MongoDB
   │
   └── Database
         │
         ├── Collection
         │      ├── Document
         │      ├── Document
         │      └── Document
         │
         └── Collection
                ├── Document
                └── Document
```

For this project:

```text
Library Database
│
├── books
├── authors
└── genres
```

---

# 4. Installation and Configuration

MongoDB can be installed locally on a computer using MongoDB Community Server.

After installation, MongoDB can be accessed through tools such as:

* MongoDB Shell (`mongosh`)
* MongoDB Compass
* Programming language drivers

For this assignment, MongoDB Shell commands are used to demonstrate database operations.

After installing MongoDB, verify that MongoDB Shell is available:

```bash
mongosh
```

If the shell starts successfully, MongoDB can be accessed through the command line.

---

# 5. Creating the Library Database

First, open MongoDB Shell:

```bash
mongosh
```

Switch to a database named `libraryDB`:

```javascript
use libraryDB
```

MongoDB creates the database when data is first inserted.

To check the current database:

```javascript
db
```

Expected result:

```text
libraryDB
```

---

# 6. Creating Collections

Create the three collections required for the library system.

## Authors Collection

```javascript
db.createCollection("authors")
```

## Genres Collection

```javascript
db.createCollection("genres")
```

## Books Collection

```javascript
db.createCollection("books")
```

To view all collections:

```javascript
show collections
```

Expected output:

```text
authors
books
genres
```

---

# 7. Database Design

The library system contains three main collections.

## Authors

```text
authors
│
├── authorId
├── name
├── country
└── birthYear
```

## Genres

```text
genres
│
├── genreId
├── name
└── description
```

## Books

```text
books
│
├── bookId
├── title
├── authorId
├── genreId
├── publishedYear
├── price
├── rating
└── available
```

The `authorId` and `genreId` fields are used to associate books with authors and genres.

---

# 8. Inserting Authors

The `insertMany()` method can be used to insert multiple documents.

```javascript
db.authors.insertMany([
    {
        authorId: 1,
        name: "R. K. Narayan",
        country: "India",
        birthYear: 1906
    },
    {
        authorId: 2,
        name: "J. K. Rowling",
        country: "United Kingdom",
        birthYear: 1965
    },
    {
        authorId: 3,
        name: "George Orwell",
        country: "United Kingdom",
        birthYear: 1903
    },
    {
        authorId: 4,
        name: "Haruki Murakami",
        country: "Japan",
        birthYear: 1949
    },
    {
        authorId: 5,
        name: "Agatha Christie",
        country: "United Kingdom",
        birthYear: 1890
    }
])
```

To view all authors:

```javascript
db.authors.find()
```

---

# 9. Inserting Genres

```javascript
db.genres.insertMany([
    {
        genreId: 1,
        name: "Fiction",
        description: "Imaginative literary works"
    },
    {
        genreId: 2,
        name: "Fantasy",
        description: "Stories involving magical or imaginary elements"
    },
    {
        genreId: 3,
        name: "Mystery",
        description: "Stories involving investigation and crime"
    },
    {
        genreId: 4,
        name: "Classic",
        description: "Important and influential literary works"
    },
    {
        genreId: 5,
        name: "Science Fiction",
        description: "Stories based on science and future technology"
    }
])
```

View the genres:

```javascript
db.genres.find()
```

---

# 10. Inserting Books

```javascript
db.books.insertMany([
    {
        bookId: 1,
        title: "Malgudi Days",
        authorId: 1,
        genreId: 1,
        publishedYear: 1943,
        price: 350,
        rating: 4.5,
        available: true
    },
    {
        bookId: 2,
        title: "Swami and Friends",
        authorId: 1,
        genreId: 4,
        publishedYear: 1935,
        price: 300,
        rating: 4.4,
        available: true
    },
    {
        bookId: 3,
        title: "Harry Potter and the Philosopher's Stone",
        authorId: 2,
        genreId: 2,
        publishedYear: 1997,
        price: 550,
        rating: 4.8,
        available: true
    },
    {
        bookId: 4,
        title: "Harry Potter and the Chamber of Secrets",
        authorId: 2,
        genreId: 2,
        publishedYear: 1998,
        price: 600,
        rating: 4.7,
        available: false
    },
    {
        bookId: 5,
        title: "1984",
        authorId: 3,
        genreId: 4,
        publishedYear: 1949,
        price: 400,
        rating: 4.7,
        available: true
    },
    {
        bookId: 6,
        title: "Animal Farm",
        authorId: 3,
        genreId: 1,
        publishedYear: 1945,
        price: 280,
        rating: 4.6,
        available: true
    },
    {
        bookId: 7,
        title: "Norwegian Wood",
        authorId: 4,
        genreId: 1,
        publishedYear: 1987,
        price: 450,
        rating: 4.3,
        available: false
    },
    {
        bookId: 8,
        title: "Murder on the Orient Express",
        authorId: 5,
        genreId: 3,
        publishedYear: 1934,
        price: 380,
        rating: 4.6,
        available: true
    }
])
```

View all books:

```javascript
db.books.find()
```

---

# 11. CRUD Operations

CRUD stands for:

```text
C → Create
R → Read
U → Update
D → Delete
```

These are the four basic operations performed on database data.

---

# 12. Create Operation

The Create operation adds new documents.

## Insert One Document

```javascript
db.books.insertOne({
    bookId: 9,
    title: "The Guide",
    authorId: 1,
    genreId: 1,
    publishedYear: 1958,
    price: 420,
    rating: 4.5,
    available: true
})
```

MongoDB returns an automatically generated `_id` along with the insertion result.

---

# 13. Read Operation

The Read operation retrieves documents.

## Display all books

```javascript
db.books.find()
```

## Display books in a readable format

```javascript
db.books.find().pretty()
```

## Find one book

```javascript
db.books.findOne({
    title: "1984"
})
```

---

# 14. Update Operation

The Update operation modifies existing documents.

For example, suppose the price of `1984` changes from ₹400 to ₹450.

```javascript
db.books.updateOne(
    { title: "1984" },
    { $set: { price: 450 } }
)
```

Verify the update:

```javascript
db.books.findOne({
    title: "1984"
})
```

---

# 15. Delete Operation

The Delete operation removes documents.

For example:

```javascript
db.books.deleteOne({
    bookId: 9
})
```

Verify that the document was deleted:

```javascript
db.books.findOne({
    bookId: 9
})
```

If it returns `null`, the document has been removed.

---

# 16. Searching Books

MongoDB provides powerful query operators for searching documents.

## 16.1 Search by Exact Title

```javascript
db.books.find({
    title: "1984"
})
```

---

## 16.2 Search Books by Author

Find books written by author ID `1`:

```javascript
db.books.find({
    authorId: 1
})
```

This returns books written by R. K. Narayan.

---

## 16.3 Search Books by Genre

Find fantasy books:

```javascript
db.books.find({
    genreId: 2
})
```

---

## 16.4 Search Books Published After 1950

```javascript
db.books.find({
    publishedYear: { $gt: 1950 }
})
```

`$gt` means **greater than**.

---

## 16.5 Search Books Published Before 1950

```javascript
db.books.find({
    publishedYear: { $lt: 1950 }
})
```

`$lt` means **less than**.

---

## 16.6 Search Books Between Two Years

```javascript
db.books.find({
    publishedYear: {
        $gte: 1950,
        $lte: 2000
    }
})
```

Here:

* `$gte` = greater than or equal to
* `$lte` = less than or equal to

---

## 16.7 Search Available Books

```javascript
db.books.find({
    available: true
})
```

---

## 16.8 Search Books with Rating Above 4.5

```javascript
db.books.find({
    rating: { $gt: 4.5 }
})
```

---

## 16.9 Search Books Below a Certain Price

Find books costing less than ₹400:

```javascript
db.books.find({
    price: { $lt: 400 }
})
```

---

## 16.10 Search by Partial Title

MongoDB supports regular expressions.

For example, to search for titles containing "Harry":

```javascript
db.books.find({
    title: { $regex: "Harry", $options: "i" }
})
```

The `i` option makes the search case-insensitive.

---

# 17. Searching Authors

## 17.1 Find Authors from India

```javascript
db.authors.find({
    country: "India"
})
```

---

## 17.2 Find Authors from the United Kingdom

```javascript
db.authors.find({
    country: "United Kingdom"
})
```

---

## 17.3 Find Authors Born Before 1900

```javascript
db.authors.find({
    birthYear: { $lt: 1900 }
})
```

---

## 17.4 Search Author by Name

```javascript
db.authors.find({
    name: "George Orwell"
})
```

---

## 17.5 Search Author Name Partially

```javascript
db.authors.find({
    name: {
        $regex: "George",
        $options: "i"
    }
})
```

---

# 18. Sorting Results

MongoDB can sort query results.

## Sort Books by Price in Ascending Order

```javascript
db.books.find().sort({
    price: 1
})
```

`1` means ascending order.

## Sort Books by Price in Descending Order

```javascript
db.books.find().sort({
    price: -1
})
```

`-1` means descending order.

---

# 19. Limiting Results

To display only the first five books:

```javascript
db.books.find().limit(5)
```

This is useful when applications need to display only a limited number of records.

---

# 20. Combining Conditions

MongoDB allows multiple conditions to be combined.

For example, find books that are available and have a rating above 4.5:

```javascript
db.books.find({
    available: true,
    rating: { $gt: 4.5 }
})
```

Another example:

```javascript
db.books.find({
    price: { $lt: 500 },
    publishedYear: { $gt: 1950 }
})
```

This searches for books costing less than ₹500 and published after 1950.

---

# 21. Counting Documents

Count the total number of books:

```javascript
db.books.countDocuments()
```

Count available books:

```javascript
db.books.countDocuments({
    available: true
})
```

Count authors from the United Kingdom:

```javascript
db.authors.countDocuments({
    country: "United Kingdom"
})
```

---

# 22. MongoDB Operators Used

| Operator | Meaning                    | Example                      |
| -------- | -------------------------- | ---------------------------- |
| `$gt`    | Greater than               | `{price: {$gt: 500}}`        |
| `$gte`   | Greater than or equal      | `{rating: {$gte: 4.5}}`      |
| `$lt`    | Less than                  | `{price: {$lt: 400}}`        |
| `$lte`   | Less than or equal         | `{year: {$lte: 2000}}`       |
| `$eq`    | Equal                      | `{country: {$eq: "India"}}`  |
| `$ne`    | Not equal                  | `{available: {$ne: false}}`  |
| `$in`    | Matches values in an array | `{genreId: {$in: [1,2]}}`    |
| `$regex` | Pattern search             | `{title: {$regex: "Harry"}}` |

---

# 23. Example Query Scenarios

### Scenario 1: Find all available books

```javascript
db.books.find({
    available: true
})
```

### Scenario 2: Find books costing less than ₹400

```javascript
db.books.find({
    price: { $lt: 400 }
})
```

### Scenario 3: Find highly rated books

```javascript
db.books.find({
    rating: { $gte: 4.7 }
})
```

### Scenario 4: Find books by R. K. Narayan

```javascript
db.books.find({
    authorId: 1
})
```

### Scenario 5: Find authors from the UK

```javascript
db.authors.find({
    country: "United Kingdom"
})
```

### Scenario 6: Find books published after 1990

```javascript
db.books.find({
    publishedYear: { $gt: 1990 }
})
```

---

# 24. Why MongoDB is Suitable for a Library System

MongoDB is suitable for this project because library data can change over time.

For example, a book may later contain additional information:

```javascript
{
    title: "1984",
    authorId: 3,
    genreId: 4,
    publishedYear: 1949,
    price: 450,
    rating: 4.7,
    available: true,
    language: "English",
    publisher: "Penguin"
}
```

MongoDB's document-oriented model makes it convenient to add fields when application requirements change.

---

# 25. Importance of NoSQL in Modern Applications

NoSQL databases have become important because modern applications often handle large amounts of diverse and rapidly changing data.

### 25.1 Flexible Data Models

NoSQL databases generally allow flexible schemas, making them useful when data structures change frequently.

### 25.2 Scalability

Many NoSQL databases are designed to scale horizontally by distributing data across multiple servers.

### 25.3 High Performance

For suitable workloads, NoSQL databases can provide fast access to large amounts of data.

### 25.4 Handling Large Data

Modern applications generate data from:

* Social media
* IoT devices
* Mobile applications
* E-commerce
* Web applications
* Streaming services

NoSQL databases are designed to support many of these large-scale workloads.

### 25.5 Modern Application Development

MongoDB is commonly used with technologies such as:

```text
React
Node.js
Express
Python
Java
```

A typical MERN application architecture is:

```text
React
  ↓
Node.js / Express
  ↓
MongoDB
```

---

# 26. Advantages of MongoDB

1. Flexible document structure
2. Easy to scale
3. JSON-like data representation
4. Powerful query language
5. Supports indexing
6. Suitable for rapidly changing applications
7. Supports aggregation
8. Easy integration with programming languages
9. Useful for large-scale applications
10. Developer-friendly data model

---

# 27. Limitations of MongoDB

MongoDB is not necessarily the best database for every application.

Some limitations include:

1. Complex relational operations may be more natural in relational databases.
2. Poorly designed document structures can create duplicated data.
3. Database design requires careful consideration of embedding and referencing.
4. Transaction-heavy applications may sometimes be better suited to relational databases.
5. Developers must understand MongoDB-specific query and indexing concepts.

Therefore, the choice between SQL and NoSQL should depend on the application's requirements.

---

# 28. SQL vs NoSQL

| Feature         | SQL                                        | NoSQL                                 |
| --------------- | ------------------------------------------ | ------------------------------------- |
| Data model      | Tables                                     | Documents/key-value/graphs/etc.       |
| Schema          | Usually fixed                              | Usually flexible                      |
| Scaling         | Commonly vertical, with horizontal options | Often designed for horizontal scaling |
| Relationships   | Strong relational support                  | Varies by database                    |
| Query language  | SQL                                        | Database-specific                     |
| Example         | MySQL                                      | MongoDB                               |
| Best suited for | Structured relational data                 | Flexible and large-scale data         |

Neither approach is universally better. The correct choice depends on the application's requirements.

---

# 29. Practical Workflow

The complete workflow for this assignment is:

```text
Install MongoDB
       ↓
Open MongoDB Shell
       ↓
Create libraryDB
       ↓
Create collections
       ↓
Insert authors
       ↓
Insert genres
       ↓
Insert books
       ↓
Perform CRUD operations
       ↓
Search and filter data
       ↓
Update records
       ↓
Delete records
       ↓
Analyze MongoDB and NoSQL
```

---

# 30. Conclusion

MongoDB is a powerful document-oriented NoSQL database that provides a flexible approach to storing and retrieving data. In this assignment, a library management database was designed with collections for books, authors, and genres.

The project demonstrated the four fundamental CRUD operations: creating, reading, updating, and deleting documents. Various MongoDB queries were also used to search books and authors according to criteria such as title, author, genre, price, rating, country, and publication year.

NoSQL databases are important in modern software development because applications increasingly need to handle large amounts of diverse and rapidly changing information. MongoDB's flexible document model and scalability make it suitable for many modern web and software applications.

However, MongoDB is not a replacement for relational databases in every situation. The appropriate database technology should be selected according to factors such as data relationships, consistency requirements, scalability, and application architecture.

---

# 31. References

1. MongoDB Documentation — MongoDB Manual
   https://www.mongodb.com/docs/

2. MongoDB Documentation — CRUD Operations
   https://www.mongodb.com/docs/manual/crud/

3. MongoDB Documentation — Query Documents
   https://www.mongodb.com/docs/manual/tutorial/query-documents/

4. MongoDB Documentation — Data Modeling
   https://www.mongodb.com/docs/manual/core/data-modeling-introduction/

5. MongoDB Documentation — MongoDB Community Edition
   https://www.mongodb.com/docs/manual/administration/install-community/

6. MongoDB Documentation — MongoDB Shell
   https://www.mongodb.com/docs/mongodb-shell/

7. MongoDB — What is NoSQL?
   https://www.mongodb.com/resources/basics/databases/nosql-explained

---

# 32. Suggested Screenshots for the Submission

To demonstrate that the practical work was actually performed, the following screenshots can be added to the GitHub README:

### Screenshot 1 — MongoDB Installation

Show MongoDB/MongoDB Shell installed successfully.

### Screenshot 2 — Database Creation

Show:

```javascript
use libraryDB
```

### Screenshot 3 — Collections

Show:

```javascript
show collections
```

with:

```text
authors
books
genres
```

### Screenshot 4 — Insert Operation

Show `insertMany()` and its successful result.

### Screenshot 5 — Read Operation

Show:

```javascript
db.books.find()
```

### Screenshot 6 — Search Query

Show one of the search queries, for example:

```javascript
db.books.find({
    rating: { $gt: 4.5 }
})
```

### Screenshot 7 — Update Operation

Show:

```javascript
db.books.updateOne(
    { title: "1984" },
    { $set: { price: 450 } }
)
```

### Screenshot 8 — Delete Operation

Show:

```javascript
db.books.deleteOne({
    bookId: 9
})
```

These screenshots provide practical evidence of the MongoDB implementation and make the GitHub submission stronger.
