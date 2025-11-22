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
   mvn clean package
java -jar target/student-task-manager.jar
mvn test

---

# statement.md (copy/paste)

---

#  Suggested folder/package structure (Java, Maven)

---
student-task-manager/
├─ README.md
├─ statement.md
├─ pom.xml
├─ src/
│ ├─ main/
│ │ ├─ java/
│ │ │ └─ com/yourname/taskmanager/
│ │ │ ├─ Main.java
│ │ │ ├─ controller/
│ │ │ │ ├─ TaskController.java
│ │ │ │ └─ DashboardController.java
│ │ │ ├─ model/
│ │ │ │ ├─ Task.java
│ │ │ │ └─ UserSettings.java
│ │ │ ├─ service/
│ │ │ │ ├─ TaskService.java
│ │ │ │ └─ ReminderService.java
│ │ │ ├─ repository/
│ │ │ │ ├─ TaskRepository.java
│ │ │ │ └─ SqliteTaskRepository.java
│ │ │ ├─ util/
│ │ │ │ ├─ CsvExporter.java
│ │ │ │ └─ DateTimeUtil.java
│ │ └─ resources/
│ │ └─ fxml/ (if JavaFX) / css / icons
│ └─ test/
│ └─ java/...
├─ docs/
│ ├─ architecture.png
│ ├─ usecase.png
│ └─ report.pdf
└─ tasks.db (or tasks.json)

#  Code Plan + Minimal class skeletons (ready to implement)
Below are Java class skeletons — implement methods as per signatures.

```java
// Task.java
package com.yourname.taskmanager.model;
import java.time.LocalDateTime;
import java.util.List;
import java.util.UUID;

public class Task {
    private String id;
    private String title;
    private String description;
    private LocalDateTime dueDateTime;
    private Priority priority;
    private Status status;
    private List<String> tags;
    private int estimatedMinutes;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;

    public Task(String title) {
        this.id = UUID.randomUUID().toString();
        this.title = title;
        this.createdAt = LocalDateTime.now();
        this.status = Status.TODO;
    }
    // getters and setters...
}

public enum Priority { LOW, MEDIUM, HIGH; }
public enum Status { TODO, IN_PROGRESS, DONE; }
// TaskRepository.java
package com.yourname.taskmanager.repository;
import com.yourname.taskmanager.model.Task;
import java.util.List;
import java.util.Optional;

public interface TaskRepository {
    Task save(Task task);
    Task update(Task task);
    boolean delete(String id);
    Optional<Task> findById(String id);
    List<Task> findAll();
    List<Task> findByFilter(TaskFilter filter);
    void exportCsv(String path);
}
// SqliteTaskRepository.java  (skeleton)
package com.yourname.taskmanager.repository;
import com.yourname.taskmanager.model.Task;
import java.util.List;
import java.util.Optional;

public class SqliteTaskRepository implements TaskRepository {
    // connection string, prepared statements
    public SqliteTaskRepository(String dbPath) { /* init connection */ }
    public Task save(Task task) { /* insert */ return task; }
    public Task update(Task task) { /* update */ return task; }
    public boolean delete(String id) { /* delete */ return true; }
    public Optional<Task> findById(String id) { return Optional.empty(); }
    public List<Task> findAll() { return List.of(); }
    public List<Task> findByFilter(TaskFilter filter) { return List.of(); }
    public void exportCsv(String path) { /* write CSV */ }
}
// TaskService.java
package com.yourname.taskmanager.service;
import com.yourname.taskmanager.model.Task;
import com.yourname.taskmanager.repository.TaskRepository;
import java.util.List;

public class TaskService {
    private final TaskRepository repo;
    private final ReminderService reminderService;

    public TaskService(TaskRepository repo, ReminderService reminder) {
        this.repo = repo;
        this.reminderService = reminder;
    }

    public Task createTask(Task t) {
        Task saved = repo.save(t);
        reminderService.scheduleReminder(saved);
        return saved;
    }
    // update, delete, list, markDone...
}


