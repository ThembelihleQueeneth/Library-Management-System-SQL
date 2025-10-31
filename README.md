Library Management System (PostgreSQL)
📚 Overview
A comprehensive SQL-based library management system designed to efficiently manage books, authors, and patrons. Built with PostgreSQL, this system provides robust functionality for library operations including inventory management, patron tracking, and advanced query capabilities.

🗂️ Database Schema
Authors Table
Stores comprehensive information about book authors.

sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    nationality VARCHAR(50),
    birth_year INT,
    death_year INT
);
Books Table
Manages book inventory with genre support and availability tracking.

sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(150),
    author_id INT REFERENCES authors(id) ON DELETE CASCADE,
    genres TEXT[],
    published_year INT,
    available BOOLEAN DEFAULT TRUE
);
Patrons Table
Tracks library patrons and their borrowed books.

sql
CREATE TABLE patrons (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    borrowed_books INT[]
);
🚀 Quick Start
Step 1: Database Creation
Open pgAdmin

Right-click on Databases → Create → Database...

Name it LibraryDB

Click Save

Step 2: Table Setup
Execute the provided SQL table creation scripts in sequence.

Step 3: Sample Data
Run the INSERT statements to populate the database with sample data.

📊 Sample Data Highlights
Featured Authors
George Orwell (British, 1903-1950)

Harper Lee (American, 1926-2016)

J.R.R. Tolkien (British, 1892-1973)

Jane Austen (British, 1775-1817)

Classic Books
*1984* by George Orwell

To Kill a Mockingbird by Harper Lee

The Great Gatsby by F. Scott Fitzgerald

Pride and Prejudice by Jane Austen

🔍 Core Operations
📖 Read Operations
sql
-- Get all books
SELECT * FROM books;

-- Find books by specific author
SELECT b.* FROM books b
JOIN authors a ON b.author_id = a.id
WHERE a.name = 'George Orwell';

-- Search available books
SELECT * FROM books WHERE available = TRUE;
✏️ Update Operations
sql
-- Mark book as borrowed
UPDATE books SET available = FALSE WHERE id = 1;

-- Add genre to existing book
UPDATE books SET genres = array_append(genres, 'Classic') WHERE id = 3;

-- Update patron's borrowed books
UPDATE patrons SET borrowed_books = array_append(borrowed_books, 9) WHERE id = 1;
🗑️ Delete Operations
sql
-- Remove book by title
DELETE FROM books WHERE title = '1984';

-- Remove author by ID
DELETE FROM authors WHERE id = 10;
🔬 Advanced Queries
Filtering & Search
sql
-- Books published after 1950
SELECT * FROM books WHERE published_year > 1950;

-- American authors
SELECT * FROM authors WHERE nationality = 'American';

-- Combined filters
SELECT * FROM books 
WHERE available = TRUE AND published_year > 1950;

-- Text search in author names
SELECT * FROM authors WHERE name ILIKE '%George%';
Batch Operations
sql
-- Reset all books to available
UPDATE books SET available = TRUE;

-- Increment publication year
UPDATE books SET published_year = published_year + 1 
WHERE published_year = 1869;
🏗️ Project Structure
text
LibraryDB/
├── Authors Table        # Author biographies and metadata
├── Books Table          # Book inventory with genres
├── Patrons Table        # Library member management
└── Operations/          # CRUD and advanced queries
💡 Key Features
✅ Array Support: PostgreSQL arrays for genres and borrowed books

✅ Referential Integrity: Foreign key constraints with cascade delete

✅ Flexible Search: ILIKE for case-insensitive text search

✅ Availability Tracking: Real-time book status monitoring

✅ Genre Management: Multiple genres per book support

🛠️ Technology Stack
Database: PostgreSQL

Interface: pgAdmin / psql

Key Features: Array types, Foreign keys, Serial IDs



Built with using PostgreSQL
