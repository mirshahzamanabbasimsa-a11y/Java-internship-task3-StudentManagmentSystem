# Java-internship-task3-StudentManagmentSystem
# Student Management System (Task 3)

A simple desktop application built in Java that lets you add, update, and view student records - built as part of my internship tasks.

## About this project

This is Task 3 of my internship. The goal was to build a basic Student Management System that could handle personal details, courses, and marks for students, with a proper GUI instead of just a console app.

I kept it intentionally simple and beginner-friendly - no database, no external libraries, just core Java and Swing - so the logic stays easy to read and follow.

## Features

- Add new student records (ID, Name, Age, Course, Marks)
- Update existing records by selecting them from the table
- Delete records
- View all records in a clean table layout
- Basic input validation (empty fields, duplicate IDs, invalid numbers)

## Tech Used

- Java
- Swing (for the GUI)
- Core OOP concepts (classes, objects, encapsulation)

## How to Run

Make sure you have JDK installed, then:

```bash
javac StudentManagementSystem.java
java StudentManagementSystem
```
OR 
Copy the code and paste it in your virtual studio code and then run it.

## What I learned

This task pushed me to think more about how the "logic" side of a program (adding/updating/storing data) connects with the "interface" side (the GUI). Handling things like table row selection, syncing the form with the table, and validating user input properly took a bit of back-and-forth, but it made the end result feel a lot more like a real, usable application rather than just a script.

## Note

This is a learning project built during my internship, so it's kept simple on purpose - single file, no persistence layer (data resets when the app closes). Happy to extend it with file/database storage in a future task.
