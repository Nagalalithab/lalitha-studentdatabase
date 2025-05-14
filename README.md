# lalitha-studentdatabase
-- Step 1: Create a database
CREATE DATABASE StudentManagement;

-- Step 2: Use the database
USE StudentManagement;

-- Step 3: Create a table for students
CREATE TABLE Students (
    StudentID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DateOfBirth DATE,
    Gender ENUM('Male', 'Female', 'Other'),
    Email VARCHAR(100),
    PhoneNumber VARCHAR(15),
    Address TEXT
);

-- Step 4: Create a table for courses
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY AUTO_INCREMENT,
    CourseName VARCHAR(100),
    Credits INT
);

-- Step 5: Create a table for enrollments (relationship between students and courses)
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY AUTO_INCREMENT,
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    Grade CHAR(2),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

-- Step 6: Insert sample data into Students table
INSERT INTO Students (FirstName, LastName, DateOfBirth, Gender, Email, PhoneNumber, Address)
VALUES
('satya', 'battina', '2003-10-09', 'Male', 'satya99@gmail.com', '1234567890', '123 Main St'),
('lalitha', 'batta', '2004-06-12', 'Female', 'lalitha77@gmail.com', '0987654321', '456 Elm St');

-- Step 7: Insert sample data into Courses table
INSERT INTO Courses (CourseName, Credits)
VALUES
('Mathematics', 3),
('Science', 4),
('History', 2);

-- Step 8: Insert sample data into Enrollments table
INSERT INTO Enrollments (StudentID, CourseID, EnrollmentDate, Grade)
VALUES
(1, 1, '2025-01-15', 'A'),
(2, 2, '2025-01-20', 'B'),
(1, 3, '2025-01-25', 'A');

-- Step 9: Query to retrieve all students
SELECT * FROM Students;

-- Step 10: Query to retrieve all courses
SELECT * FROM Courses;

-- Step 11: Query to retrieve all enrollments with student and course details
SELECT 
    Enrollments.EnrollmentID,
    Students.FirstName,
    Students.LastName,
    Courses.CourseName,
    Enrollments.EnrollmentDate,
    Enrollments.Grade
FROM 
    Enrollments
JOIN 
    Students ON Enrollments.StudentID = Students.StudentID
JOIN 
    Courses ON Enrollments.CourseID = Courses.CourseID;

-- Step 12: Update a student record
UPDATE Students
SET Email = 'updated.email@example.com'
WHERE StudentID = 1;

-- Step 13: Delete a course
DELETE FROM Courses
WHERE CourseID = 3;
