# Experiment 1: Entity-Relationship (ER) Diagram
## Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.
## Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.


## Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).


### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.



## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Ranen Joseph Solomon(212224040269)

## Scenario Chosen:
Scenario 1: University Database

## ER Diagram:
<img width="2884" height="726" alt="Complete University Database ER Diagram (1)" src="https://github.com/user-attachments/assets/dbd0c5dd-ebee-4215-8cca-19a2a4b45b8f" />

## Entities and Attributes

### 1. **Student**
- **Attributes**:
  - `student_id` (PK): Unique identifier for each student.
  - `first_name`: First name of the student.
  - `last_name`: Last name of the student.
  - `dob`: Date of birth of the student.
  - `contact_info`: Contact information such as phone number, email, and address.
  - `program_id` (FK): Foreign Key referencing the Program the student is enrolled in.

- **Purpose**: Represents individual students in the university.



### 2. **Instructor**
- **Attributes**:
  - `instructor_id` (PK): Unique identifier for each instructor.
  - `first_name`: First name of the instructor.
  - `last_name`: Last name of the instructor.
  - `contact_info`: Contact details (phone number, email, etc.).
  - `department_id` (FK): Foreign Key referencing the department the instructor belongs to.

- **Purpose**: Represents instructors who teach courses.



### 3. **Department**
- **Attributes**:
  - `department_id` (PK): Unique identifier for each department.
  - `department_name`: Name of the department (e.g., Computer Science).
  - `department_head` (FK): Foreign Key referencing the instructor who heads the department.

- **Purpose**: Represents departments that offer various programs and courses.



### 4. **Program**
- **Attributes**:
  - `program_id` (PK): Unique identifier for each program (e.g., BSc in Computer Science).
  - `program_name`: Name of the program.
  - `department_id` (FK): Foreign Key referencing the department offering the program.

- **Purpose**: Represents academic programs offered by the university.



### 5. **Course**
- **Attributes**:
  - `course_id` (PK): Unique identifier for each course.
  - `course_number` (Unique): Unique course number.
  - `course_name`: Name of the course (e.g., Data Structures).
  - `credits`: Number of credits for the course.
  - `department_id` (FK): Foreign Key referencing the department offering the course.

- **Purpose**: Represents individual courses that students can enroll in.



### 6. **Prerequisite**
- **Attributes**:
  - `course_id` (FK): Foreign Key referencing a course.
  - `prerequisite_course_id` (FK): Foreign Key referencing a prerequisite course.

- **Purpose**: Models the relationship between courses and their prerequisites.



### 7. **Enrollment**
- **Attributes**:
  - `enrollment_id` (PK): Unique identifier for each enrollment record.
  - `student_id` (FK): Foreign Key referencing the student.
  - `course_id` (FK): Foreign Key referencing the course the student is enrolled in.
  - `enrollment_date`: Date when the student enrolled in the course.

- **Purpose**: Tracks which students are enrolled in which courses.


## Relationships and Constraints:
### 1. **Student - Program**
- **Cardinality**: One student belongs to one program, but a program can have many students (1:M).
- **Participation**: Mandatory for students (each student must be enrolled in a program). Optional for programs (a program can have zero or many students).
- **Description**: Each student is enrolled in a specific academic program (e.g., BSc in Computer Science).



### 2. **Program - Department**
- **Cardinality**: One program is offered by one department, but a department can offer many programs (1:M).
- **Participation**: Mandatory for programs (every program must belong to a department).
- **Description**: A program is part of a specific department (e.g., Computer Science program belongs to the Department of Computer Science).



### 3. **Course - Department**
- **Cardinality**: One course is offered by one department, but a department can offer many courses (1:M).
- **Participation**: Mandatory for courses (every course must belong to a department).
- **Description**: A course is offered under a specific department (e.g., Data Structures course offered by the Computer Science Department).



### 4. **Course - Prerequisite**
- **Cardinality**: A course can have multiple prerequisites, and a prerequisite can be required by multiple courses (M:N).
- **Participation**: Optional for courses (not every course has prerequisites).
- **Description**: Some courses require other courses as prerequisites (e.g., "Algorithms" may require "Data Structures" as a prerequisite).



### 5. **Student - Enrollment - Course**
- **Cardinality**: A student can enroll in many courses, and a course can have many students (M:N).
- **Participation**: Mandatory for both students (students must enroll in courses) and courses (courses must have enrolled students).
- **Description**: Tracks the enrollment of students in various courses.


### 6. **Instructor - Course**
- **Cardinality**: One instructor can teach many courses, and a course can be taught by multiple instructors (M:N).
- **Participation**: Optional for instructors (not all instructors teach courses every semester).
- **Description**: Instructors are assigned to teach specific courses.


## Modeling Prerequisites

- **Prerequisite Entity**: This entity captures the relationship between courses and their prerequisite courses. Each record in this table specifies a course and its associated prerequisite(s). A course may have one or many prerequisite courses.
  
- **Foreign Keys**: The `course_id` and `prerequisite_course_id` in the **Prerequisite** table are foreign keys that reference the **Course** entity, establishing the prerequisite relationship.


## ER Diagram Flowchart Format

Here’s a flowchart structure for the ER diagram, which you can implement in **draw.io** or any other tool:

```plaintext
[Student] ---<enrolled_in>--- [Program] ---<offered_by>--- [Department] ---<offers>--- [Course] ---<has_prerequisite>--- [Course (Prerequisite)]
   |                               |                               |
   |                               |                               |
   v                               v                               v
[Enrollment]                     [Instructor]                     [Department Head]
```
## Flowchart Explanation

- **Student** is linked to **Program** through an "enrolled_in" relationship.
- **Program** is linked to **Department** through an "offered_by" relationship.
- **Department** offers multiple **Courses**.
- **Courses** can have prerequisites, creating a **has_prerequisite** relationship linking a course to its required courses.
- **Instructor** is linked to **Course**, as instructors teach multiple courses.

## Conclusion

### **Entities**:
The database consists of **Student**, **Instructor**, **Department**, **Program**, **Course**, **Prerequisite**, and **Enrollment**.

### **Relationships**:
We have **many-to-many** and **one-to-many** relationships between students, programs, courses, departments, and prerequisites.

### **Prerequisites**:
The **Prerequisite** entity tracks the courses required before others, ensuring proper course sequencing.
