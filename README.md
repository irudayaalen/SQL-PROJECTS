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

# 1. To find students enrolled in a specific course (e.g., CourseID = 101):

SELECT s.FirstName, s.LastName, e.EnrollmentDate
FROM Students s
JOIN Enrollments e ON s.student_id = e.StudentID
WHERE e.CourseID = 101;

# 2. To find courses offered by a specific department (e.g., DepartmentID = 2):

SELECT c.CourseName, c.Credits
FROM Courses c
WHERE c.DepartmentID = 2;




# 3. To update the major of a specific student (e.g., StudentID = 101):

UPDATE Students
SET Major = 'Data Science'
WHERE student_id = 101;

# 4. Retrieve a list of students along with the courses they are enrolled in.

SELECT s.FirstName, s.LastName, c.CourseName
FROM Students s
JOIN Enrollments e ON s.student_id = e.StudentID
JOIN Courses c ON e.CourseID = c.CourseID;

# 5. Get a list of all students and the courses they are enrolled in, including students who are not enrolled in any courses.

SELECT s.FirstName, s.LastName, c.CourseName
FROM Students s
LEFT JOIN Enrollments e ON s.student_id = e.StudentID
LEFT JOIN Courses c ON e.CourseID = c.CourseID;

# 6. Get a list of all courses and the students enrolled in them, including courses that have no students enrolled.

SELECT c.CourseName, s.FirstName, s.LastName
FROM Courses c
RIGHT JOIN Enrollments e ON c.CourseID = e.CourseID
RIGHT JOIN Students s ON e.StudentID = s.student_id;

# 7. Get a list of all students and all courses, including students not enrolled in any courses and courses with no students enrolled.

SELECT s.FirstName, s.LastName, c.CourseName
FROM Students s
LEFT JOIN Enrollments e ON s.student_id = e.StudentID
LEFT JOIN Courses c ON e.CourseID = c.CourseID
UNION
SELECT s.FirstName, s.LastName, c.CourseName
FROM Courses c
LEFT JOIN Enrollments e ON c.CourseID = e.CourseID
LEFT JOIN Students s ON e.StudentID = s.student_id;

# 8. Combining Courses and Departments
SELECT CourseName AS Name, 'Course' AS Type
FROM Courses

UNION

SELECT DepartmentName AS Name, 'Department' AS Type
FROM Departments;

# 9. Create a view that displays each professor's name and their department name.

CREATE VIEW ProfessorDepartments AS
SELECT p.FirstName, p.LastName, d.DepartmentName
FROM Professors p
JOIN Departments d ON p.DepartmentID = d.DepartmentID;

# 10. Create a stored procedure that retrieves the list of students enrolled in a given course by CourseID.
DELIMITER //

CREATE PROCEDURE GetStudentsByCourse(IN courseID INT)
BEGIN
    SELECT s.FirstName, s.LastName
    FROM Students s
    JOIN Enrollments e ON s.student_id = e.StudentID
    WHERE e.CourseID = courseID;
END //

DELIMITER ;

# 11. Retrieve a list of courses sorted by the number of credits in descending order.

SELECT CourseName, Credits
FROM Courses
ORDER BY Credits DESC;

# 12. Count the total number of students.

SELECT COUNT(*) AS TotalStudents
FROM Students;

# 13. Calculate the average number of credits for all courses.

SELECT AVG(Credits) AS AverageCredits
FROM Courses;

# 14. Get the maximum and minimum number of credits among courses.

SELECT MAX(Credits) AS MaxCredits, MIN(Credits) AS MinCredits
FROM Courses;

# 15. Count the number of professors in each department.

SELECT d.DepartmentName, COUNT(p.ProfessorID) AS NumberOfProfessors
FROM Professors p
JOIN Departments d ON p.DepartmentID = d.DepartmentID
GROUP BY d.DepartmentName;
