# Experiment 1: Entity-Relationship (ER) Diagram

## Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

##  Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
University

## ER Diagram:
<img width="1194" height="616" alt="ER Diagram" src="https://github.com/user-attachments/assets/4d20bd60-f786-4340-b20e-41b5df388cbc" />

## Entities and Attributes:
- Student: Student Name, Register Number, Age, DOB, Year
- Department: Name, Faculties, Lab
- Enrollment: Course Code, Credits
- Course: Name, Course Code, Faculty, Domain, Prerequisites
- Faculty: Name, Department

## Relationships and Constraints:
- Student — Belongs To — Department
Cardinality: Many-to-One (Many students belong to one department)

Participation: Total (Every student must belong to a department)

- Student — Does — Enrollment
Cardinality: One-to-Many (A student can have many enrollment records)

Participation: Total (If a student is taking courses, they must be enrolled)

- Enrollment — Has — Course
Cardinality: Many-to-One (Each enrollment is for one course, but each course can have many enrollments)

Participation: Total on Enrollment (An enrollment must be for a course)

- Student — Enrolls — Course
Cardinality: Many-to-Many (A student can enroll in many courses, and a course can have many students)

Participation: Partial

- Course — Teaches — Faculty
Cardinality: Many-to-One (Each course is taught by one faculty, a faculty can teach many courses)

Participation: Total on Course

- Faculty — Belongs To — Department
Cardinality: Many-to-One (Each faculty member belongs to one department)

## Extension (Prerequisite / Billing):
- A course can have one or more other courses as prerequisites.

- This is represented using a many-to-many recursive relationship.

## Design Choices:

- Student, Course, Faculty, Department are fundamental academic components.

- Enrollment is a bridge entity for a many-to-many relationship between Students and Courses, while also capturing enrollment metadata (e.g., credits, prerequisites).

- Department helps in structuring programs and associating faculty and students.

## RESULT
- The ER model accurately represents an academic system with students, courses, faculty, departments, enrollments, and supports prerequisites through a recursive course relationship.

