# Saidatta-s-first-SQL-project
-- =============================================
-- Project: Library Management System
-- Author: Sai Datta
-- Description: A database to manage library books, authors, and members.
-- =============================================

-- Step 1: Create the Database
CREATE DATABASE LibraryDB;
GO

-- Use the Database
USE LibraryDB;
GO

-- =============================================
-- Step 2: Create Tables
-- =============================================

-- Create Authors Table
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY IDENTITY(1,1),
    FirstName NVARCHAR(50) NOT NULL,
    LastName NVARCHAR(50) NOT NULL,
    BirthDate DATE
);
GO

-- Create Books Table
CREATE TABLE Books (
    BookID INT PRIMARY KEY IDENTITY(1,1),
    Title NVARCHAR(100) NOT NULL,
    AuthorID INT,
    PublicationYear INT,
    Genre NVARCHAR(50),
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);
GO

-- Create Members Table
CREATE TABLE Members (
    MemberID INT PRIMARY KEY IDENTITY(1,1),
    FullName NVARCHAR(100) NOT NULL,
    MembershipDate DATE,
    Email NVARCHAR(100)
);
GO

-- =============================================
-- Step 3: Insert Sample Data
-- =============================================

-- Insert Authors
INSERT INTO Authors (FirstName, LastName, BirthDate)
VALUES 
('George', 'Orwell', '1903-06-25'),
('Jane', 'Austen', '1775-12-16'),
('Mark', 'Twain', '1835-11-30');
GO

-- Insert Books
INSERT INTO Books (Title, AuthorID, PublicationYear, Genre)
VALUES
('1984', 1, 1949, 'Dystopian'),
('Pride and Prejudice', 2, 1813, 'Romance'),
('The Adventures of Huckleberry Finn', 3, 1884, 'Adventure');
GO

-- Insert Members
INSERT INTO Members (FullName, MembershipDate, Email)
VALUES
('Alice Johnson', '2023-01-15', 'alice@example.com'),
('Bob Smith', '2023-02-20', 'bob@example.com'),
('Charlie Brown', '2023-03-05', 'charlie@example.com');
GO

-- =============================================
-- Step 4: Query the Data
-- =============================================

-- Retrieve all authors
SELECT * FROM Authors;
GO

-- Retrieve all books
SELECT * FROM Books;
GO

-- Retrieve all members
SELECT * FROM Members;
GO

-- =============================================
-- Step 5: Example Advanced Queries (Optional)
-- =============================================

-- Show all books with their authors
SELECT 
    B.Title AS BookTitle,
    CONCAT(A.FirstName, ' ', A.LastName) AS AuthorName,
    B.PublicationYear,
    B.Genre
FROM Books B
JOIN Authors A ON B.AuthorID = A.AuthorID;
GO

-- Show total number of members
SELECT COUNT(*) AS TotalMembers FROM Members;
GO

-- Find books published before 1900
SELECT Title, PublicationYear FROM Books WHERE PublicationYear < 1900;
GO
