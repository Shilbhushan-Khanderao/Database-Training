# Database

## Queries used in Session

### 1. DDL (Data Definition Language)

#### CREATE Table

   ```sql
   CREATE TABLE Students (
       StudentID INT PRIMARY KEY,
       FirstName VARCHAR(50),
       LastName VARCHAR(50),
       DateOfBirth DATE,
       Address VARCHAR(100)
   );
   ```

   ```sql
   CREATE TABLE OldStudentRecords (
       RecordID INT PRIMARY KEY,
       StudentID INT,
       RecordDetails TEXT
   );
   ```

   ```sql
   CREATE TABLE Courses (
       CourseID INT PRIMARY KEY,
       CourseName VARCHAR(50) NOT NULL,
       Credits INT NOT NULL
   );
   ```

   ```sql
   CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseID INT,
    Grade DECIMAL(3, 2),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
   ```

#### Alter Table

   ```sql
   ALTER TABLE Students
   ADD Email VARCHAR(50);
   ```

#### Truncate Table

   ```sql
   TRUNCATE TABLE OldStudentRecords;
   ```

#### Drop Table

   ```sql
   DROP TABLE OldStudentRecords;
   ```

### 2. DML (Data Manipulation Language)

#### Insert Data

   ```sql
   INSERT INTO Students 
   VALUES (1, 'Ashish', 'Nikam', '2005-09-01', '123 Shivaji Nagar, Jalgaon', 'ashish.nikam@example.com');

   INSERT INTO Students (StudentID, FirstName, LastName, DateOfBirth, Address, Email)
   VALUES 
   (2, 'Vinod', 'Patil', '2006-02-10', 'Laxmi Road, Pune', 'vinod.patil@example.com'),
   (3, 'Raj', 'Shinde', '2007-03-15', '101 Maple   Street, Nagpur', 'raj.shinde@example.com'),
   (4, 'Sonali', 'Deshmukh', '2005-04-20', '011 Kala Ghoda Chowk, Mumbai', 'sonali.deshmukh@example.com'),
   (5, 'Priya', 'Jadhav', '2008-05-25', '303 College Road, Nashik', 'priya.jadhav@example.com');
```

   ```sql
   INSERT INTO Courses
   VALUES (1, 'Mathematics', 3);

   INSERT INTO Courses (CourseID, CourseName, Credits)
   VALUES 
   (2, 'Science', 4),
   (3, 'History', 3),
   (4, 'English', 3),
   (5, 'Computer', 2);
   ```

   ```sql
   INSERT INTO Enrollments
   VALUES (1, 1, 1, 3.5);

   INSERT INTO Enrollments (EnrollmentID, StudentID, CourseID, Grade)
   VALUES 
   (2, 2, 2, 3.8), -- Vinod Patil enrolled in Science with Grade 3.8
   (3, 3, 3, 3.0), -- Raj Shinde enrolled in History with Grade 3.0
   (4, 4, 4, 3.7), -- Sonali Deshmukh enrolled in English with Grade 3.7
   (5, 5, 5, 4.0), -- Priya Jadhav enrolled in Physical Education with Grade 4.0
   (6, 1, 2, 3.6), -- Alice Johnson enrolled in Science with Grade 3.6
   (7, 2, 3, 3.9), -- Vinod Patil enrolled in History with Grade 3.9
   (8, 3, 4, 3.2); -- Raj Shinde enrolled in English with Grade 3.2
   ```

#### Update Data

   ```sql
   UPDATE Students
   SET Address = 'Mahesh Nagar, Jalgaon'
   WHERE StudentID = 1;
   ```

#### Delete Data

   ```sql
   DELETE FROM Students
   WHERE StudentID = 1;
   ```

### 3. DQL (Data Query Language)

#### Select Data

   ```sql
   SELECT FirstName, LastName, Address
   FROM Students
   WHERE DateOfBirth > '2005-01-01';
   ```

### 4. Constraints

#### CREATE TABLE Courses with NOT NULL

   ```sql
   CREATE TABLE Courses (
       CourseID INT PRIMARY KEY,
       CourseName VARCHAR(50) NOT NULL,
       Credits INT NOT NULL
   );
   ```

#### CREATE TABLE Students with UNIQUE Email

   ```sql
   CREATE TABLE Students (
       StudentID INT PRIMARY KEY,
       FirstName VARCHAR(50),
       LastName VARCHAR(50),
       DateOfBirth DATE,
       Address VARCHAR(100),
       Email VARCHAR(50) UNIQUE
   );
   ```

#### CREATE TABLE Classes with PRIMARY KEY

   ```sql
   CREATE TABLE Classes (
       ClassID INT PRIMARY KEY,
       ClassName VARCHAR(50)
   );
   ```

#### CREATE TABLE Enrollments with FOREIGN KEY

   ```sql
   CREATE TABLE Enrollments (
       EnrollmentID INT PRIMARY KEY,
       StudentID INT,
       CourseID INT,
       FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
       FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
   );
   ```

#### CREATE TABLE Grades with CHECK Constraint

   ```sql
   CREATE TABLE Grades (
       StudentID INT PRIMARY KEY,
       Grade DECIMAL(3, 2),
       CHECK (Grade BETWEEN 0 AND 4.0)
   );
   ```

### 5. Clauses

#### WHERE Clause with LIKE

   ```sql
   SELECT FirstName, LastName
   FROM Students
   WHERE Address LIKE '%Elm St%';
   ```

#### ORDER BY Clause

   ```sql
   SELECT FirstName, LastName
   FROM Students
   ORDER BY LastName ASC;
   ```

#### GROUP BY Clause

   ```sql
   SELECT COUNT(*), Address
   FROM Students
   GROUP BY Address;
   ```

#### LIMIT Clause

   ```sql
   SELECT FirstName, LastName
   FROM Students
   LIMIT 10;
   ```

### 6. Operators

#### AND Operator

   ```sql
   SELECT FirstName, LastName
   FROM Students
   WHERE Address LIKE '%St%' AND DateOfBirth > '2005-01-01';
   ```

#### OR Operator

   ```sql
   SELECT FirstName, LastName
   FROM Students
   WHERE Address LIKE '%Elm%' OR Address LIKE '%Maple%';
   ```

#### LIKE Operator

   ```sql
   SELECT FirstName, LastName
   FROM Students
   WHERE LastName LIKE 'J%';
   ```

#### BETWEEN Operator

   ```sql
   SELECT FirstName, LastName
   FROM Students
   WHERE DateOfBirth BETWEEN '2000-01-01' AND '2005-12-31';
   ```

### 7. Aggregate Functions

#### COUNT()

   ```sql
   SELECT COUNT(*)
   FROM Students;
   ```

#### AVG()

   ```sql
   SELECT AVG(Grade)
   FROM Grades;
   ```

#### SUM()

   ```sql
   SELECT SUM(Credits)
   FROM Courses;
   ```

#### MIN()

   ```sql
   SELECT MIN(DateOfBirth)
   FROM Students;
   ```

#### MAX()

   ```sql
   SELECT MAX(DateOfBirth)
   FROM Students;
   ```

### 8. Joins

#### INNER JOIN

   ```sql
   SELECT Students.FirstName, Students.LastName, Courses.CourseName
   FROM Students
   INNER JOIN Enrollments ON Students.StudentID = Enrollments.StudentID
   INNER JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
   ```

#### LEFT JOIN

   ```sql
   SELECT Students.FirstName, Students.LastName, Grades.Grade
   FROM Students
   LEFT JOIN Grades ON Students.StudentID = Grades.StudentID;
   ```

#### RIGHT JOIN

   ```sql
   SELECT Courses.CourseName, Students.FirstName, Students.LastName
   FROM Courses
   RIGHT JOIN Enrollments ON Courses.CourseID = Enrollments.CourseID
   RIGHT JOIN Students ON Enrollments.StudentID = Students.StudentID;
   ```

#### FULL OUTER JOIN

   ```sql
   SELECT Students.FirstName, Students.LastName, Courses.CourseName
   FROM Students
   FULL OUTER JOIN Enrollments ON Students.StudentID = Enrollments.StudentID
   FULL OUTER JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
   ```

#### SELF JOIN

   ```sql
   SELECT A.FirstName AS MentorFirstName, B.FirstName AS MenteeFirstName
   FROM Students A, Students B
   WHERE A.StudentID = B.MentorID;
   ```
