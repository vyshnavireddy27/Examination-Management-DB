# 🎓 University Academic Management Database

This relational database system manages data related to departments, faculty members, students, courses, and exams at a university. It supports academic operations like course offerings, faculty assignments, and exam management.

---

## 🏛️ Database Tables Overview

### 📁 `department` Table

| Column Name | Data Type | Description                           |
|-------------|------------|---------------------------------------|
| dept_id     | INT (PK)   | Unique department ID                  |
| dept_name   | VARCHAR    | Name of the department                |
| head_id     | INT (FK)   | Faculty member heading the department (refers to `faculty.faculty_id`) |

---

### 📁 `faculty` Table

| Column Name | Data Type | Description                           |
|-------------|------------|---------------------------------------|
| faculty_id  | INT (PK)   | Unique faculty/employee ID            |
| name        | VARCHAR    | Faculty name                          |
| designation | VARCHAR    | Designation (e.g., Professor, HOD)    |

---

### 📁 `course` Table

| Column Name | Data Type     | Description                                 |
|-------------|---------------|---------------------------------------------|
| course_code | VARCHAR (PK)  | Unique identifier for the course            |
| title       | VARCHAR       | Name/title of the course                    |
| dept_id     | INT (FK)      | Department offering the course (`department.dept_id`) |

---

### 📁 `student` Table

| Column Name | Data Type | Description                                  |
|-------------|-----------|----------------------------------------------|
| roll_number | INT (PK)  | Unique student roll number                   |
| name        | VARCHAR   | Name of the student                          |
| dept_id     | INT (FK)  | Department student belongs to (`department.dept_id`) |

---

### 📁 `exam` Table

| Column Name  | Data Type     | Description                                    |
|--------------|---------------|------------------------------------------------|
| exam_id      | INT (PK)      | Unique ID of the exam                         |
| title        | VARCHAR       | Title of the exam                             |
| subject_name | VARCHAR       | Subject of the exam (matches course title)    |
| duration     | INT           | Duration in minutes                           |
| date         | DATE          | Date of the exam                              |
| type         | VARCHAR       | Internal or External                          |
| course_code  | VARCHAR (FK)  | Course the exam is for (`course.course_code`) |
| faculty_id   | INT (FK)      | Creator of the exam (`faculty.faculty_id`)    |

---

## 🔗 Relationships

- Each **department** is headed by a **faculty** member.
- A **faculty** can create multiple **exams**.
- A **course** is offered by one **department**.
- An **exam** is linked to both a **course** and its **faculty** creator.
- A **student** belongs to one **department**.

---

## 🛠️ Features & Concepts Used

- Primary Keys (PK) and Foreign Keys (FK)
- 1:N relationships (e.g., department to courses, faculty to exams)
- Data normalization
- Academic data integrity enforcement

---

## 📌 Use Case Examples

- Track courses offered by each department
- Assign department heads from faculty members
- Link exams to faculty and courses
- Query students by department
- Retrieve internal vs. external exam data

---

## 🚀 Sample Queries You Can Run

```sql
-- Get all exams created by a particular faculty
SELECT * FROM exam WHERE faculty_id = 101;

-- List courses offered by 'Computer Science' department
SELECT course.title FROM course
JOIN department ON course.dept_id = department.dept_id
WHERE department.dept_name = 'Computer Science';

-- Show all students from the 'Mechanical' department
SELECT name FROM student
JOIN department ON student.dept_id = department.dept_id
WHERE department.dept_name = 'Mechanical';
```

---


