# 📚 Library Management System (PostgreSQL)

A simple yet powerful **SQL-based Library Management System** designed to manage **books, authors, and patrons** efficiently.  
This project demonstrates the use of **PostgreSQL** for relational database design, data manipulation, and advanced queries.

---

## 🚀 Project Overview

This project is built to help a library manage:
- **Books** in their collection (with details such as title, author, genre, publication year, and availability).
- **Authors** and their details.
- **Patrons** who borrow books.

Users can **add, view, update, and delete** records, while maintaining proper **relationships between tables** using foreign keys.

---

## 🧱 Sprint 1: Project Setup

### Step 1 — Create the Database
In **pgAdmin**:
1. Right-click on **Databases → Create → Database...**
2. Name it **`LibraryDB`**
3. Click **Save**

### Step 2 — Create the Tables

```
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    nationality VARCHAR(50),
    birth_year INT,
    death_year INT
);



CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(150),
    author_id INT REFERENCES authors(id) ON DELETE CASCADE,
    genres TEXT[],
    published_year INT,
    available BOOLEAN DEFAULT TRUE
);

CREATE TABLE patrons (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    borrowed_books INT[]
);
```
### 🌱 Sprint 2: Insert Sample Data
## Authors

```
]INSERT INTO authors (id, name, nationality, birth_year, death_year)
VALUES
(1, 'George Orwell', 'British', 1903, 1950),
(2, 'Harper Lee', 'American', 1926, 2016),
(3, 'F. Scott Fitzgerald', 'American', 1896, 1940),
(4, 'Aldous Huxley', 'British', 1894, 1963),
(5, 'J.D. Salinger', 'American', 1919, 2010),
(6, 'Herman Melville', 'American', 1819, 1891),
(7, 'Jane Austen', 'British', 1775, 1817),
(8, 'Leo Tolstoy', 'Russian', 1828, 1910),
(9, 'Fyodor Dostoevsky', 'Russian', 1821, 1881),
(10, 'J.R.R. Tolkien', 'British', 1892, 1973);

```

## Books

```
INSERT INTO books (id, title, author_id, genres, published_year, available)
VALUES
(1, '1984', 1, ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
(2, 'To Kill a Mockingbird', 2, ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
(3, 'The Great Gatsby', 3, ARRAY['Tragedy'], 1925, TRUE),
(4, 'Brave New World', 4, ARRAY['Dystopian', 'Science Fiction'], 1932, TRUE),
(5, 'The Catcher in the Rye', 5, ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
(6, 'Moby-Dick', 6, ARRAY['Adventure Fiction'], 1851, TRUE),
(7, 'Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
(8, 'War and Peace', 8, ARRAY['Historical Novel'], 1869, TRUE),
(9, 'Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866, TRUE),
(10, 'The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);
```

##Patrons

```
INSERT INTO patrons (id, name, email, borrowed_books)
VALUES
(1, 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
(2, 'Bob Smith', 'bob@example.com', ARRAY[1, 2]),
(3, 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
(4, 'David Brown', 'david@example.com', ARRAY[3]),
(5, 'Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
(6, 'Frank Moore', 'frank@example.com', ARRAY[4, 5]),
(7, 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
(8, 'Hank Wilson', 'hank@example.com', ARRAY[6]),
(9, 'Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
(10, 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);

```

### 🔍 Sprint 3: Read Operations (Queries)
## Get All Books

```
SELECT * FROM books;
Get a Book by Title

SELECT * FROM books WHERE title = '1984';
```

Get All Books by a Specific Author

```

SELECT b.* 
FROM books b 
JOIN authors a ON b.author_id = a.id 
WHERE a.name = 'George Orwell';
```

Get All Available Books

```
SELECT * FROM books WHERE available = TRUE;
```

🛠️ Sprint 4: Update Operations
Mark a Book as Borrowed

```UPDATE books
 SET available = FALSE
 WHERE id = 1;
```

Add a New Genre to an Existing Book

``` UPDATE books
SET genres = array_append(genres, 'Classic')
 WHERE id = 3;```

Add a Borrowed Book to a Patron’s Record

UPDATE patrons SET borrowed_books = array_append(borrowed_books, 9) WHERE id = 1;

❌ Sprint 5: Delete Operations

Delete a Book by Title
DELETE FROM books WHERE title = '1984';

Delete an Author by ID
DELETE FROM authors WHERE id = 10;

🧠 Sprint 6: Advanced Queries
Find Books Published After 1950

SELECT * FROM books WHERE published_year > 1950;
Find All American Authors

SELECT * FROM authors WHERE nationality = 'American';
Set All Books as Available

UPDATE books SET available = TRUE;
Find All Available Books Published After 1950

SELECT * FROM books WHERE available = TRUE AND published_year > 1950;
Find Authors Whose Names Contain "George"

SELECT * FROM authors WHERE name ILIKE '%George%';
Increment Published Year (Example: Update 1869 → 1870)


UPDATE books SET published_year = published_year + 1 WHERE published_year = 1869;
🧩 Database Relationships
Table	Relationship	Description
authors → books	One-to-Many	Each author can have multiple books.
books → patrons	Many-to-Many (via borrowed_books array)	A patron can borrow multiple books.

💡 Key Learnings
Use of PostgreSQL arrays (TEXT[], INT[]) for flexible data handling.

Foreign key constraints with ON DELETE CASCADE to maintain referential integrity.

Real-world CRUD (Create, Read, Update, Delete) operations.

Use of JOINs and advanced queries for data exploration.

🧑‍💻 Author
Thembelihle Maluka
📍Polokwane South Africa
💻 Passionate about full-stack software development.

