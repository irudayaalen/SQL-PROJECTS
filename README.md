# SQL-PROJECTS
# College Database Managemnt System

use sqlprojects;
Create table Students (
    student_id int primary key,
    firstname varchar(50),
    lastname varchar(50),
    Dateofbirth DATE,
    major varchar(50));
    
    INSERT INTO Students (student_id, firstname, lastname, DateOfBirth, major)
VALUES 
(101, 'Alice', 'Green', '2002-01-15', 'Computer Science'),
(102, 'Bob', 'Brown', '2002-02-20', 'Mathematics'),
(103, 'Charlie', 'Smith', '2002-03-25', 'Biology'),
(104, 'Diana', 'Johnson', '2002-04-30', 'Chemistry'),
(105, 'Eve', 'Davis', '2002-05-05', 'Physics'),
(106, 'Frank', 'Miller', '2002-06-10', 'Engineering'),
(107, 'Grace', 'Wilson', '2002-07-15', 'Economics'),
(108, 'Henry', 'Moore', '2002-08-20', 'Philosophy'),
(109, 'Ivy', 'Taylor', '2002-09-25', 'Psychology');

select*from students;
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    DepartmentID INT,
    Credits int
);
INSERT INTO Courses (CourseID, CourseName, DepartmentID, Credits)
VALUES 
(101, 'Introduction to Programming', 1, 3),
(102, 'Calculus I', 2, 4),
(103, 'General Biology', 3, 4),
(104, 'Organic Chemistry', 4, 4),
(105, 'Classical Mechanics', 5, 3),
(106, 'Data Structures', 1, 3),
(107, 'Linear Algebra', 2, 4),
(108, 'Genetics', 3, 4),
(109, 'Physical Chemistry', 4, 3);

select*from courses;
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    Student_id INT,
    CourseID INT,
    EnrollmentDate DATE,
    FOREIGN KEY (Student_id) REFERENCES Students(Student_id),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

INSERT INTO Enrollments (EnrollmentID, Student_id, CourseID, EnrollmentDate)
VALUES 
(101, 101, 101, '2024-01-15'),
(102, 102, 102, '2024-01-16'),
(103, 102, 103, '2024-01-17'),
(104, 103, 103, '2024-01-18'),
(105, 103, 105, '2024-01-19'),
(106, 105, 105, '2024-01-20'),
(107, 107, 107, '2024-01-21'),
(108, 108, 108, '2024-01-22'),
(109, 109, 109, '2024-01-23');
select*from enrollments;
create table Professors (
    ProfessorID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DepartmentID INT
);
INSERT INTO Professors (ProfessorID, FirstName, LastName, DepartmentID)
VALUES 
(101, 'James', 'Anderson', 1),
(102, 'Linda', 'Taylor', 2),
(103, 'Robert', 'Clark', 3),
(104, 'Patricia', 'Wilson', 4),
(105, 'Michael', 'Moore', 5),
(106, 'Jennifer', 'White', 1),
(107, 'William', 'Lewis', 2),
(108, 'Elizabeth', 'Walker', 3),
(109, 'David', 'Harris', 4);
select*from professors;

Create table  Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100)
);
INSERT INTO Departments (DepartmentID, DepartmentName)
VALUES 
(101, 'Computer Science'),
(102, 'Mathematics'),
(103, 'Biology'),
(104, 'Chemistry'),
(105, 'Physics'),
(106, 'Engineering'),
(107, 'Economics'),
(108, 'Philosophy'),
(109, 'Psychology');
