# Student Management System (Java CLI) ⭐

An Object-Oriented, command-line Student Management System written in standard Java. This application provides student record management, subject score tracking, and automated 10-point CGPA and letter grade computation.

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Key Features](#key-features)
3. [Object-Oriented Architecture](#object-oriented-architecture)
4. [Prerequisites & Environment Setup](#prerequisites--environment-setup)
5. [Step-by-Step Compilation & Execution](#step-by-step-compilation--execution)
   - [Windows (PowerShell / Command Prompt)](#windows-powershell--command-prompt)
   - [macOS / Linux (Terminal)](#macos--linux-terminal)
6. [CLI Navigation & Feature Guide](#cli-navigation--feature-guide)
7. [Grading & CGPA Calculation Logic](#grading--cgpa-calculation-logic)
8. [Project Structure](#project-structure)
9. [Troubleshooting](#troubleshooting)

---

## 📖 Project Overview

The **Student Management System** is a standalone terminal application designed to manage student academic records. Built using standard Java without third-party libraries, it demonstrates core Object-Oriented Programming and Java programming concepts:

- **Classes & Objects**: Models students and their academic information.
- **Inheritance & Polymorphism**: Uses an abstract `Person` class and a specialized `Student` class.
- **Encapsulation**: Protects object data using private fields and controlled access.
- **Dynamic Collections (`ArrayList`)**: Stores student records in memory.
- **Input Validation**: Validates user input and handles invalid entries through the utility layer.
- **CLI Application Design**: Provides an interactive menu-driven terminal interface.

---

## ✨ Key Features

1. **Add Student**: Register a student with ID, name, email, contact number, course/branch, semester, and subject marks.
2. **Delete Student**: Remove a student record by ID with a confirmation step.
3. **Search Student**:
   - Search by Student ID.
   - Search by name using case-insensitive partial matching.
4. **Update Student Details**: Modify student information and subject marks.
5. **Display All Students**: View student records in a formatted table.
6. **Calculate Grades & CGPA**: Calculate subject-wise grades, overall percentage, 10-point CGPA, and academic standing.
7. **Pre-Loaded Sample Data**: Includes sample student records for testing the application immediately after launch.
8. **Reset / Reload Sample Data**: Restore the default sample dataset.

---

## 🏗️ Object-Oriented Architecture

The project is organized into separate model, service, utility, and driver components.

### `model.Person`
Abstract base class containing common person-related information:

- `name`
- `email`
- `contactNumber`
- Abstract method `displayDetails()`

### `model.Student`
Extends `Person` and represents a student.

Contains student-specific information such as:

- `studentId`
- `course`
- `semester`
- `subjectMarks`
- `cgpa`
- `grade`

It also handles student-specific display and academic calculations.

### `service.StudentManager`

Acts as the business-logic layer.

- Maintains student records using `ArrayList<Student>`.
- Handles adding and deleting students.
- Performs student searches.
- Updates student information.
- Manages sample data.

### `util.InputValidator`

Handles command-line input validation and helps prevent invalid input from terminating the program unexpectedly.

### `Main`

The main driver class responsible for:

- Starting the application.
- Displaying the menu.
- Reading user choices.
- Routing the selected operation.

---

## ⚙️ Prerequisites & Environment Setup

### 1. Java Development Kit (JDK)

A Java Development Kit is required to compile and run the project.

Check whether Java is installed:

```bash
javac -version
java -version
```

If both commands return a Java version, the JDK is available.

### 2. Installing Java

If Java is not installed, install a JDK appropriate for your operating system.

- **Windows**: Oracle JDK or Eclipse Temurin
- **macOS**: OpenJDK / Eclipse Temurin
- **Linux**: OpenJDK through the distribution package manager

Make sure the Java `bin` directory is added to your system `PATH` so that `java` and `javac` can be used from a terminal.

---

## 🚀 Step-by-Step Compilation & Execution

The project does not require Maven or Gradle. It can be compiled directly using the Java compiler (`javac`).

> **Important:** Run the commands from the **project root directory** — the folder that contains `Main.java`, `model`, `service`, and `util`.

### Windows (PowerShell / Command Prompt)

1. Open **Command Prompt** or **PowerShell**.

2. Navigate to the project root directory:

   ```cmd
   cd "<PROJECT_DIRECTORY>"
   ```

   Replace `<PROJECT_DIRECTORY>` with the location of the project on your computer.

3. Compile the Java source files:

   ```cmd
   javac model\Person.java model\Student.java service\StudentManager.java util\InputValidator.java Main.java
   ```

4. Run the application:

   ```cmd
   java Main
   ```

### macOS / Linux (Terminal)

1. Open a terminal.

2. Navigate to the project root directory:

   ```bash
   cd "<PROJECT_DIRECTORY>"
   ```

3. Compile the Java source files:

   ```bash
   javac model/Person.java model/Student.java service/StudentManager.java util/InputValidator.java Main.java
   ```

4. Run the application:

   ```bash
   java Main
   ```

### IntelliJ IDEA

The project can also be opened directly in **IntelliJ IDEA**:

1. Open IntelliJ IDEA.
2. Select **Open** and choose the project root directory.
3. Make sure the installed JDK is selected under the project settings.
4. Open `Main.java`.
5. Run the `Main` class.

---

## 🖥️ CLI Navigation & Feature Guide

Upon launching, the application displays an interactive menu similar to:

```text
============================================================
          WELCOME TO STUDENT MANAGEMENT SYSTEM
============================================================
[*] Pre-loaded sample student records for testing.

------------------------------------------------------------
                      MAIN MENU
------------------------------------------------------------
  1. Add Student
  2. Delete Student
  3. Search Student (by ID or Name)
  4. Update Student Details
  5. Display All Students
  6. Calculate & View Student Grades / CGPA
  7. Reset / Reload Sample Data
  8. Exit Application
------------------------------------------------------------
Enter your choice (1-8):
```

### Quick Walkthrough of Menu Actions

- **Option 1 (Add Student)**: Adds a new student and accepts academic details and subject marks.
- **Option 2 (Delete Student)**: Deletes a student after confirmation.
- **Option 3 (Search Student)**: Searches using Student ID or name.
- **Option 4 (Update Student Details)**: Updates student information or subject marks.
- **Option 5 (Display All Students)**: Displays all current student records.
- **Option 6 (Calculate & View Grades/CGPA)**: Displays marks, percentage, CGPA, and grade information.
- **Option 7 (Reset / Reload Sample Data)**: Restores the default sample records.
- **Option 8 (Exit)**: Safely exits the application.

---

## 📊 Grading & CGPA Calculation Logic

The grading engine uses a 10-point CGPA calculation based on the average percentage.

### 1. Cumulative Grade Point Average (CGPA)

Given `N` subjects with individual percentage scores `Sᵢ`:

$$
\text{Average Percentage} =
\frac{\sum_{i=1}^{N} S_i}{N}
$$

$$
\text{CGPA} =
\frac{\text{Average Percentage}}{10.0}
$$

The resulting CGPA is rounded to two decimal places.

### 2. Letter Grade Scale

| Percentage Range | 10-Point Scale | Letter Grade | Academic Standing |
|:----------------:|:--------------:|:------------:|:-----------------:|
| 90.0% – 100.0%   | 9.00 – 10.00   | **A+**       | Outstanding       |
| 80.0% – 89.9%    | 8.00 – 8.99    | **A**        | Excellent         |
| 70.0% – 79.9%    | 7.00 – 7.99    | **B+**       | Very Good         |
| 60.0% – 69.9%    | 6.00 – 6.99    | **B**        | Good              |
| 50.0% – 59.9%    | 5.00 – 5.99    | **C**        | Average           |
| 40.0% – 49.9%    | 4.00 – 4.99    | **D**        | Pass              |
| Below 40.0%      | Below 4.00     | **F**        | Fail              |

---

## 📁 Project Structure

The project root contains the following files and directories:

```text
Programming in java/
├── .idea/                  # IntelliJ IDEA project configuration
├── model/                  # Data/model classes
│   ├── Person.java
│   └── Student.java
├── service/                # Business logic
│   └── StudentManager.java
├── util/                   # Utility and input-validation classes
│   └── InputValidator.java
├── .gitignore              # Git ignore configuration
├── Main.java               # Application entry point
└── Main.class              # Compiled Main class (generated)
```

> **Note:** `.class` files are generated when the Java source files are compiled. They are not source files and generally do not need to be committed to GitHub.

---

## 🔧 Troubleshooting

### `javac` is not recognized / `javac: command not found`

The JDK may not be installed or its `bin` directory may not be included in the system `PATH`.

Verify with:

```bash
javac -version
```

### `ClassNotFoundException: Main`

Make sure you are running the command from the **project root directory**, where `Main.java` is located:

```bash
java Main
```

Also make sure the compilation step completed successfully.

### Package / Class Compilation Errors

Compile the source files from the project root rather than from inside `model`, `service`, or `util`.

For example:

```bash
javac model/Person.java model/Student.java service/StudentManager.java util/InputValidator.java Main.java
```

### Invalid Input While Using the CLI

The project includes the `InputValidator` utility to validate and handle user input. When invalid input is entered, the program can prompt the user again instead of terminating immediately.

---

## 👤 Author

Developed as a Java Object-Oriented Programming project.
