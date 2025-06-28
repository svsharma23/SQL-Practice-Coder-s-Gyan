# SQL Query Practice – Coder’s Gyan
This repository contains solutions to 10 SQL problems based on the **Coders Gyan SQL series**.
The project focuses on improving SQL skills through real-world-style queries.



**1. SQL: List departments in alphabetical order**
You are given a database table named departments with the following columns:
id (Integer): The unique identifier for each department.
name (String): The department’s name.
Write a SQL query that returns the id and name of every department, sorted by the department’s name in ascending (alphabetical) order. Your result should include all rows
from the departments table.

**Answer** 
SELECT id, name
FROM departments
ORDER BY name ;


**2. SQL: List All Instructors in a Department**
You are given two database tables:
departments: Stores department details.
id (INTEGER, Primary Key)
name (TEXT, Department Name)
instructors: Stores instructor details.
id (INTEGER, Primary Key)
name (TEXT, Instructor’s Name)
email (TEXT, Instructor’s Email)
department_id (INTEGER, Foreign Key referencing departments(id))
Write an SQL query to list all instructors in a specific department. The result should include:
instructor_id: The unique ID of the instructor
instructor_name: The name of the instructor
email: The instructor’s email
The query should filter instructors by a given department ID (1).

**Answer**
SELECT id, name, email
FROM instructors
WHERE department_id = 1;



**3. SQL: Find the Department of an Instructor**
You are given two database tables:
departments: Stores department details.
id (INTEGER, Primary Key)
name (TEXT, Department Name)
instructors: Stores instructor details.
id (INTEGER, Primary Key)
name (TEXT, Instructor’s Name)
email (TEXT, Instructor’s Email)
department_id (INTEGER, Foreign Key referencing departments(id))
Write an SQL query to find the department an instructor belongs to. The result should include:
department_id: The unique ID of the department
department_name: The name of the department
The query should filter by a given instructor ID: 7

**Answer**
SELECT id, name
FROM departments
WHERE id = 7;


**4. SQL: Find All Courses a Student is Enrolled In**
You are given three database tables:
students: Stores student details.
id (INTEGER, Primary Key)
name (TEXT, Student’s Name)
email (TEXT, Student’s Email)
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
enrollments: Pivot table that links students and courses (Many-to-Many).
student_id (INTEGER, Foreign Key referencing students(id))
course_id (INTEGER, Foreign Key referencing courses(id))
Write an SQL query to find all courses a specific student is enrolled in. The result should include:
course_id: The unique ID of the course
course_name: The name of the course
The query should filter by a given student ID: 4

**Answer**
SELECT c.id AS course_id, c.name AS course_name
FROM enrollments e
INNER JOIN courses c
ON e.course_id = c.id
WHERE e.student_id = 4;


**5. SQL: List All Courses with Instructor Names**
You are given two database tables:
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
instructor_id (INTEGER, Foreign Key referencing instructors(id))
instructors: Stores instructor details.
id (INTEGER, Primary Key)
name (TEXT, Instructor’s Name)
Write an SQL query to list all courses along with their respective instructors. The result should include:
course_id: The unique ID of the course
course_name: The name of the course
instructor_name: The name of the instructor teaching the course
The result should be sorted in alphabetical order by course_name.

**Answer**
SELECT
c.id AS course_id,
c.name AS course_name,
i.name AS instructor_name
FROM courses c
JOIN instructors i
ON c.instructor_id = i.id
ORDER BY c.name;



**6. SQL: Get a Specific Course with Department & Instructor Info**
You are given three database tables:
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
syllabus (TEXT, Course Syllabus)
instructor_id (INTEGER, Foreign Key referencing instructors(id))
department_id (INTEGER, Foreign Key referencing departments(id))
instructors: Stores instructor details.
id (INTEGER, Primary Key)
name (TEXT, Instructor’s Name)
departments: Stores department details.
id (INTEGER, Primary Key)
name (TEXT, Department Name)
Write an SQL query to get details of a specific course by its ID, along with the department and instructor information.
The result should include:
course_id: The unique ID of the course
course_name: The name of the course
syllabus: The course syllabus
instructor_id: The unique ID of the instructor
instructor_name: The name of the instructor
department_id: The unique ID of the department
department_name: The name of the department
The query should filter by a given course ID : 9


**Answer**
SELECT
c.id AS course_id,
c.name AS course_name,
c.syllabus AS syllabus,
i.id AS instructor_id,
i.name AS instructor_name,
d.id AS department_id,
d.name AS department_name
FROM courses c
INNER JOIN instructors i
ON c.instructor_id = i.id
INNER JOIN departments d
ON c.department_id = d.id
WHERE c.id = 9;


**7. SQL: List All Students Enrolled in a Particular Course**
You are given two database tables:
students: Stores student details.
id (INTEGER, Primary Key)
name (TEXT, Student’s Name)
enrollments: Pivot table that links students and courses (Many-to-Many).
student_id (INTEGER, Foreign Key referencing students(id))
course_id (INTEGER, Foreign Key referencing courses(id))
Write an SQL query to list all students enrolled in a specific course. The result should include:
student_id: The unique ID of the student
student_name: The name of the student
The query should filter by a given course ID: 3

**Answer**
SELECT
s.id AS student_id,
s.name AS student_name
FROM students s
INNER JOIN enrollments e
ON s.id = e.student_id
WHERE e.course_id = 3;


**8. SQL: Find Student Enrollment Count for Each Course**
You are given three database tables:
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
enrollments: Pivot table that links students and courses (Many-to-Many).
student_id (INTEGER, Foreign Key referencing students(id))
course_id (INTEGER, Foreign Key referencing courses(id))
students: Stores student details.
id (INTEGER, Primary Key)
name (TEXT, Student’s Name)
Write an SQL query to find the total number of students enrolled in each course. The result should include:
course_id: The unique ID of the course
course_name: The name of the course
total_students: The number of students enrolled in the course
The result should be sorted in alphabetical order by course_name.

**Answer**
SELECT
c.id AS course_id,
c.name AS course_name,
COUNT(e.student_id) AS total_students
FROM courses c
INNER JOIN enrollments e
ON c.id = e.course_id
GROUP BY c.id, c.name
ORDER BY c.name;



**9. SQL: Find the Instructor Who Teaches the Most Courses**
You are given two database tables:
instructors: Stores instructor details.
id (INTEGER, Primary Key)
name (TEXT, Instructor’s Name)
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
instructor_id (INTEGER, Foreign Key referencing instructors(id))
Write an SQL query to find the instructor who teaches the most courses. The result should include:
instructor_id: The unique ID of the instructor
instructor_name: The name of the instructor
total_courses: The number of courses taught by that instructor
The result should be sorted in descending order of total courses, and only the top instructor should be returned.

**Answer**
SELECT
i.id AS instructor_id,
i.name AS instructor_name,
COUNT(c.id) AS total_courses
FROM instructors i
INNER JOIN courses c
ON i.id = c.instructor_id
GROUP BY i.id, i.name
ORDER BY total_courses DESC;



**10. SQL: Find Courses with No Students Enrolled**
You are given two database tables:
courses: Stores course details.
id (INTEGER, Primary Key)
name (TEXT, Course Name)
enrollments: Pivot table that links students and courses (Many-to-Many).
student_id (INTEGER, Foreign Key referencing students(id))
course_id (INTEGER, Foreign Key referencing courses(id))
Write an SQL query to find all courses that have no students enrolled. The result should include:
course_id: The unique ID of the course
course_name: The name of the course
Only courses without enrollments should be returned.

**Answer**
SELECT
c.id AS course_id,
c.name AS course_name
FROM courses c
LEFT JOIN enrollments e
ON c.id = e.course_id
WHERE e.student_id IS NULL;






