# Student Task Manager

## Overview
Student Task Manager is a lightweight Java desktop application that helps students manage tasks, deadlines, reminders and track progress. Built using Java (JavaFX optional) with a modular architecture following MVC.

## Features
- Create, edit, delete tasks
- Task priorities, tags, and status (ToDo / InProgress / Done)
- Due date/time and reminder scheduling
- Dashboard with task counts and completion rate
- Search and filter tasks
- Export tasks to CSV
- Local persistence (SQLite or JSON)

## Technologies
- Java 11+ (recommended Java 17)
- JavaFX (for GUI) OR console fallback
- SQLite (via JDBC) or JSON file persistence
- JUnit for unit testing
- Maven or Gradle for build

## Installation
1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd student-task-manager
