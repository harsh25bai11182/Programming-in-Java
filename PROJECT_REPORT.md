# PROJECT REPORT: STUDENT MANAGEMENT SYSTEM

---

## 1. Executive Summary / Abstract

The **Student Management System** is a standalone terminal application developed in Java that demonstrates core and intermediate Object-Oriented Programming (OOP) principles. It provides functionality for maintaining student records, managing contact details and academic information, storing subject marks, computing a project-defined 10-point CGPA, and assigning letter grades based on percentage ranges. Designed without third-party library dependencies, the system emphasizes input validation, encapsulation, modular design, and reliable command-line interaction.

---

## 2. Introduction & Problem Statement

In educational environments, managing student information and academic performance manually or across separate records can lead to data-entry errors, inconsistent updates, and calculation mistakes.

The primary objective of this project is to develop a console-driven Java application that provides:

- Controlled modification of student data through object-oriented encapsulation.
- Dynamic storage of student records using Java Collections (`ArrayList`).
- Menu-driven command-line navigation with input validation.
- Automated calculation of percentage, CGPA, and letter grade.

---

## 3. Functional Requirements

The system provides the following major functional modules:

1. **Student Record Management**
   - Add new student records.
   - Delete student records.
   - Display all student records.

2. **Student Search & Update**
   - Search students by Student ID.
   - Search students by name.
   - Update personal and academic details.
   - Add or update subject marks.

3. **Academic Evaluation**
   - Calculate average percentage.
   - Calculate the project-defined 10-point CGPA.
   - Assign a letter grade based on the implemented percentage ranges.
   - Display academic results.

4. **Input Validation & Sample Data Management**
   - Validate user input through `InputValidator`.
   - Prevent invalid mark values and invalid data types.
   - Load and reset sample student data.

---

## 4. Non-Functional Requirements

The system is designed with the following non-functional requirements:

### 4.1 Usability

- Provides an interactive, menu-driven command-line interface.
- Uses clear prompts and structured output for common operations.
- Provides validation messages when user input is invalid.

### 4.2 Reliability

- Validates numeric input and mark ranges before processing.
- Prevents duplicate Student IDs where required by the application.
- Uses controlled input handling to reduce unexpected termination during normal invalid-input scenarios.

### 4.3 Maintainability

- Separates responsibilities into `model`, `service`, and `util` packages.
- Keeps student data models, business logic, input validation, and CLI coordination in separate classes.
- Uses object-oriented design so individual components can be modified with limited impact on unrelated components.

### 4.4 Resource Efficiency

- Uses in-memory Java collections for the current implementation.
- Does not require a database or third-party libraries.
- Performs record and subject operations using standard Java collections.

---

## 5. Core Concepts & Object-Oriented Design

The system demonstrates the following Java and software engineering concepts:

### 3.1 Classes and Objects

- Real-world entities are represented through domain classes such as `Person` and `Student`.
- Data and related behavior are organized within their respective classes.

### 3.2 Abstraction

- The `Person` abstract class represents common personal information such as `name`, `email`, and `contactNumber`.
- It declares the abstract method `displayDetails()`, which subclasses implement according to their specific requirements.

### 3.3 Inheritance

- The `Student` class extends `Person`.
- It inherits common personal information and adds student-specific information such as `studentId`, `course`, `semester`, `subjectMarks`, `cgpa`, and `grade`.
- This models an "is-a" relationship between `Student` and `Person`.

### 3.4 Polymorphism

- The `displayDetails()` method declared in `Person` is overridden in `Student`.
- When a `Student` object is referenced through a `Person` reference, the overridden `Student` implementation is invoked at runtime.

### 3.5 Encapsulation

- Data members are kept private and accessed through methods provided by the classes.
- Validation is applied to relevant input and mutator operations.
- Marks are restricted to the range **0.0 to 100.0 inclusive**.

### 3.6 Collections Framework (`ArrayList` & `LinkedHashMap`)

- `ArrayList<Student>` is used by `StudentManager` to maintain a dynamic collection of student records.
- `LinkedHashMap<String, Double>` is used for subject marks, allowing subjects to retain insertion order while supporting key-based score access and updates.

### 3.7 Control Flow & Error Handling

- Menu processing uses `switch` statements and `while` loops.
- Console input is processed through `InputValidator` to handle invalid data types, numeric ranges, and common `Scanner` input issues.

---

## 4. Class & Module Architecture

```text
                           +-------------------+
                           |   <<abstract>>    |
                           |      Person       |
                           +-------------------+
                           | - name: String    |
                           | - email: String   |
                           | - contactNumber   |
                           +-------------------+
                           | + displayDetails()|
                           +---------^---------+
                                     |
                                  extends
                                     |
                           +---------+---------+
                           |      Student      |
                           +-------------------+
                           | - studentId       |
                           | - course          |
                           | - semester        |
                           | - subjectMarks    |
                           | - cgpa            |
                           | - grade           |
                           +-------------------+
                           | + computeCGPA()   |
                           | + displayDetails()|
                           +-------------------+
                                     ^
                                     |
                                  manages
                                     |
                           +---------+----------+
                           |   StudentManager   |
                           +--------------------+
                           | - students: List  |
                           +--------------------+
                           | + addStudent()    |
                           | + deleteStudent() |
                           | + findStudentById()|
                           | + displayAll()    |
                           +--------------------+

        +-----------------------+            uses
        |    InputValidator     | <------------------- Main
        +-----------------------+                      |
        | + readString()        |                      |
        | + readInt()           |                      |
        | + readDouble()        |                      |
        | + readEmail()         |                      |
        | + readPhoneNumber()   |                      |
        +-----------------------+                      v
                                               +----------------+
                                               |      Main      |
                                               +----------------+
                                               | + main()       |
                                               | + printMenu()  |
                                               +----------------+
```

### Module Descriptions

1. **`model.Person`**
   - **Fields:** `name`, `email`, `contactNumber`.
   - **Responsibilities:** Stores common personal information and defines the abstract `displayDetails()` contract.

2. **`model.Student`**
   - **Fields:** `studentId`, `course`, `semester`, `subjectMarks`, `cgpa`, `grade`.
   - **Responsibilities:** Maintains student academic information, calculates grades/CGPA, and displays student details.

3. **`service.StudentManager`**
   - **Fields:** `List<Student> students`.
   - **Responsibilities:** Manages student records, including adding, deleting, searching, updating, and sample-data handling.

4. **`util.InputValidator`**
   - **Responsibilities:** Handles console input validation, numeric range checks, and email/phone validation.

5. **`Main` / `Main.java`**
   - **Responsibilities:** `Main.java` is the application's entry-point source file. Its `main()` method starts the CLI, displays the menu, accepts user choices, and coordinates the application workflow.

---

## 5. Algorithmic Formulations

### 5.1 Cumulative Grade Point Average (CGPA)

The project uses the following 10-point CGPA calculation:

$$
\text{Average Percentage } (P) =
\frac{\sum_{i=1}^{N} \text{Mark}_i}{N}
$$

$$
\text{CGPA} =
\frac{P}{10.0}
\quad
(\text{rounded to 2 decimal places})
$$

This is the calculation implemented for the project's academic evaluation logic and should not be interpreted as a universal CGPA formula used by every university.

### 5.2 Letter Grade Classification Matrix

| Percentage Range | 10-Point Range | Letter Grade | Academic Standing |
|---|---:|---|---|
| $90.0\% \le P \le 100.0\%$ | 9.00 – 10.00 | **A+** | Outstanding |
| $80.0\% \le P < 90.0\%$ | 8.00 – 8.99 | **A** | Excellent |
| $70.0\% \le P < 80.0\%$ | 7.00 – 7.99 | **B+** | Very Good |
| $60.0\% \le P < 70.0\%$ | 6.00 – 6.99 | **B** | Good |
| $50.0\% \le P < 60.0\%$ | 5.00 – 5.99 | **C** | Average |
| $40.0\% \le P < 50.0\%$ | 4.00 – 4.99 | **D** | Pass |
| $P < 40.0\%$ | Below 4.00 | **F** | Fail |

---

## 6. Functional Verification & Test Scenarios

The following test scenarios were used to verify the main functional units of the application:

| Test ID | Test Scenario | Input Data | Expected Output | Status |
|---|---|---|---|---|
| **TC-01** | Add Student with Valid Details | ID: `STU105`, Name: `Rajesh Kumar`, Course: `Data Science`, Sem: `1`, Marks: `95.0, 91.0` | Student enrolled, CGPA calculated as `9.30`, Grade `A+` | **PASSED** |
| **TC-02** | Add Student with Duplicate ID | ID: `STU101` (already present) | Duplicate-ID validation message and request for another ID | **PASSED** |
| **TC-03** | Search Student by Exact ID | ID: `STU101` | Corresponding student profile is displayed | **PASSED** |
| **TC-04** | Search Student by Partial Name | Name: `diya` | Matching student record is displayed irrespective of letter case | **PASSED** |
| **TC-05** | Update Student Details | Change name to `Diya P. Sharma`, add subject `Advanced Algorithms (95)` | Student details are updated and CGPA is recalculated | **PASSED** |
| **TC-06** | Delete Student with Confirmation | ID: `STU103`, Confirmation: `y` | Student record is removed | **PASSED** |
| **TC-07** | Display All Students | Display operation | Formatted student table is generated | **PASSED** |
| **TC-08** | Input Type Validation | Text entered when an integer is expected | Validation message is shown and the input is requested again | **PASSED** |
| **TC-09** | Out-of-bounds Mark Entry | Mark: `105.0` or `-5.0` | Validation message stating that marks must be between `0.0` and `100.0` | **PASSED** |

---

## 7. Build and Execution Instructions

The project uses standard Java and does not require Maven, Gradle, or third-party libraries.

> **Important:** Run the commands below from the **project root directory**, which is the folder containing `Main.java`, `model`, `service`, and `util`.

### Windows (PowerShell / Command Prompt)

```cmd
javac model\Person.java model\Student.java service\StudentManager.java util\InputValidator.java Main.java
java Main
```

### macOS / Linux (Terminal)

```bash
javac model/Person.java model/Student.java service/StudentManager.java util/InputValidator.java Main.java
java Main
```

### IntelliJ IDEA

The project can be run directly from IntelliJ IDEA:

1. Open the project root directory.
2. Make sure a JDK is configured for the project.
3. Open **`Main.java`**.
4. Run the **`Main` class**.

`Main.java` contains the `public static void main(String[] args)` method and is the entry point of the application.

---

## 8. Project Structure

The project root is organized as follows:

```text
Programming in java/
├── .idea/                  # IntelliJ IDEA project configuration
├── model/
│   ├── Person.java         # Abstract base class
│   └── Student.java        # Student model and academic logic
├── service/
│   └── StudentManager.java # Student record management
├── util/
│   └── InputValidator.java # Console input validation
├── .gitignore              # Git ignore rules
├── Main.java               # Application entry point
├── README.md
└── PROJECT_REPORT.md
```

---

## 9. Conclusion

The **Student Management System** demonstrates the practical use of Encapsulation, Inheritance, Polymorphism, Abstraction, Java Collections, control flow, and input validation in a terminal-based Java application. Its modular organization separates model classes, business logic, input utilities, and the application entry point, making the project easier to understand and maintain.
