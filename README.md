# 📚  Education based system

## 📌 Project Overview

This project is a **University Course Enrollment and Student Grading System** built in Java. It demonstrates strong Object-Oriented Programming (OOP) design, robust exception handling, Java Collections, and Generics & Wildcards.

The system manages:
- Student registration and profiles
- Course registration and capacity management
- Student enrollment in courses with duplicate prevention
- Grade assignment with validation
- Academic performance tracking and GPA calculation

---

## 🎯 Objectives

- Model real-world university entities using OOP principles
- Enforce business rules through custom exception handling
- Use Java Collections for data management and integrity
- Implement Generic classes and Wildcard methods for type safety and reusability
- Build an interactive menu-driven system with full input validation

---

## 🏗️ Project Structure

```
UniversityEnrollmentSystem/
│
├── entities/
│   ├── Person.java              (Abstract base class)
│   ├── Student.java             (Student entity)
│   ├── Instructor.java          (Instructor entity)
│   ├── Course.java              (Course entity)
│   └── Enrollment.java          (Links Student and Course)
│
├── exceptions/
│   ├── UniversitySystemException.java       (Base custom exception)
│   ├── DuplicateEnrollmentException.java    (Duplicate enrollment error)
│   ├── InvalidGradeException.java           (Invalid grade error)
│   ├── StudentNotFoundException.java        (Student not found error)
│   ├── CourseNotFoundException.java         (Course not found error)
│   └── NotEnrolledException.java            (Not enrolled error)
│
├── services/
│   ├── Repository.java          (Generic interface)
│   ├── GenericRepository.java   (Generic implementation)
│   ├── StudentService.java      (Student business logic)
│   ├── CourseService.java       (Course business logic)
│   └── EnrollmentService.java   (Enrollment business logic)
│
└── Main.java                    (Interactive menu-driven entry point)
```

---

## 🧠 OOP Concepts Implemented

### 1. Encapsulation
- All fields are declared `private`
- Access controlled through getters and setters
- Input validation inside setter methods

### 2. Abstraction
- `Person` is an abstract class
- Contains abstract methods `getRole()` and `displayInfo()`
- Forces subclasses to provide their own implementation

### 3. Inheritance
- `Student` extends `Person`
- `Instructor` extends `Person`
- Reuses common properties like name, email, and ID

### 4. Polymorphism
- `displayInfo()` behaves differently for Student and Instructor
- Demonstrated using a `Person[]` array in Main

### 5. Relationship Modeling
- Student HAS-MANY Enrollments (One-to-Many)
- Course HAS-MANY Enrollments (One-to-Many)
- Enrollment LINKS Student and Course (Many-to-Many Association)
- Instructor HAS-MANY Courses (One-to-Many)

### 6. Separation of Concerns
- Entity classes handle data only
- Service classes handle business logic
- Main class handles user interaction
- Exception classes handle error reporting

---

## ⚠️ Exception Handling

### Custom Exception Hierarchy

```
RuntimeException (Java built-in - Unchecked)
└── UniversitySystemException (Custom base exception)
    ├── DuplicateEnrollmentException
    ├── InvalidGradeException
    ├── StudentNotFoundException
    ├── CourseNotFoundException
    └── NotEnrolledException
```

### Business Rules Enforced

| Rule | Exception Thrown |
|------|-----------------|
| Student cannot enroll in the same course twice | `DuplicateEnrollmentException` |
| Grade must be between 0.0 and 5.0 | `InvalidGradeException` |
| Cannot enroll non-existent student | `StudentNotFoundException` |
| Cannot enroll in non-existent course | `CourseNotFoundException` |
| Cannot grade a student not enrolled in the course | `NotEnrolledException` |
| Cannot enroll when course is full | `UniversitySystemException` |
| Cannot register duplicate student or course | `UniversitySystemException` |

---

## 📦 Java Collections Usage

| Collection | Where Used | Purpose |
|-----------|-----------|---------|
| `ArrayList` | Student, Course, Enrollment lists | Ordered storage of entities |
| `HashMap` | GenericRepository | Fast O(1) lookup by ID |
| `List` interface | Service return types | Flexible collection handling |
| `Optional` | Repository findById | Safe null handling |

---

## 🔧 Generics & Wildcards

### Generic Interface
```java
public interface Repository<T> {
    void add(T entity);
    Optional<T> findById(String id);
    List<T> findAll();
    boolean exists(String id);
}
```

### Generic Class
```java
public class GenericRepository<T> implements Repository<T> {
    private Map<String, T> storage;
    // Works with Student, Course, or any entity type
}
```

### Upper Bounded Wildcard
```java
public void addAll(List<? extends T> entities) {
    // Accepts any list of T or its subclasses
}
```

### Lower Bounded Wildcard
```java
public void exportTo(List<? super T> destination) {
    // Exports to any list of T or its parent classes
}
```

### Generic Methods with Predicates
```java
public List<T> findWhere(Predicate<T> condition) {
    // Finds entities matching any condition
}

public int countWhere(Predicate<? super T> condition) {
    // Counts entities matching any condition
}
```

---

## 📊 GPA Scale (0 - 5)

| GPA Range | Letter Grade | Classification |
|-----------|-------------|----------------|
| 4.5 - 5.0 | A+ | First Class Honours |
| 4.0 - 4.4 | A | First Class Honours |
| 3.5 - 3.9 | B+ | Second Class Upper |
| 3.0 - 3.4 | B | Second Class Lower |
| 2.5 - 2.9 | C+ | Second Class Lower |
| 2.0 - 2.4 | C | Pass |
| 1.5 - 1.9 | D | Pass |
| 1.0 - 1.4 | E | Fail |
| 0.0 - 0.9 | F | Fail |

---

## 🖥️ Interactive Menu

```
╔════════════════════════════════════════════╗
║            MAIN MENU                       ║
╚════════════════════════════════════════════╝
  1. Register Student
  2. Register Course
  3. Enroll Student in Course
  4. Assign Grade to Student
  5. View All Students
  6. View All Courses
  7. View Student Details
  8. View Course Details
  9. View Student Academic Summary
 10. View System Statistics
  0. Exit
```

---

## ✅ Input Validation

| Input Type | Validation Rules |
|-----------|-----------------|
| Student ID | Cannot be empty |
| Student Name | Letters, spaces, and hyphens only |
| Email | Must contain '@' and '.' with valid format |
| Credit Hours | Must be between 1 and 6 |
| Course Capacity | Must be between 1 and 100 |
| Grade | Must be between 0.0 and 5.0 |
| Menu Choice | Must be a valid number within range |

---

## ▶️ How to Run the Project

### Compile

```bash
javac Main.java
```

### Run

```bash
java Main
```

---

## 🧪 Test Scenarios

### Test 1: Happy Path
1. Register 3 students
2. Register 2 courses
3. Enroll students in courses
4. Assign grades
5. View academic summaries and statistics

### Test 2: Duplicate Enrollment Prevention
1. Register a student and a course
2. Enroll the student in the course
3. Try to enroll the same student in the same course again
4. System catches `DuplicateEnrollmentException`

### Test 3: Course Full Prevention
1. Register a course with capacity of 2
2. Enroll 2 students successfully
3. Try to enroll a 3rd student
4. System catches `UniversitySystemException` with COURSE_FULL error

### Test 4: Invalid Grade Prevention
1. Enroll a student in a course
2. Try to assign a grade above 5.0 or below 0.0
3. System catches `InvalidGradeException`

### Test 5: Not Enrolled Prevention
1. Register a student and a course
2. Try to assign a grade without enrolling first
3. System catches `NotEnrolledException`

### Test 6: Non-existent Entity Prevention
1. Try to enroll a non-existent student (e.g., ID: S999)
2. System catches `StudentNotFoundException`
3. Try to enroll in a non-existent course (e.g., Code: CS999)
4. System catches `CourseNotFoundException`

---

## 📁 Requirements

- Java 8 or higher
- No external libraries required

---

## 📈 Evaluation Criteria Coverage

| Criteria | Marks | How It's Demonstrated |
|----------|-------|----------------------|
| **Class Design & Structure** | 2.5 | 5 entity + 5 service classes with clear responsibilities |
| **Encapsulation** | 2.5 | All fields private with controlled access |
| **Inheritance & Abstraction** | 2.5 | Person abstract class with Student and Instructor |
| **Relationship Modeling** | 5 | Student-Enrollment, Course-Enrollment, Instructor-Course |
| **Separation of Concerns** | 2.5 | Entity, Service, Exception, and Main layers |
| **Custom Exceptions** | 0.5 | 6 custom exceptions with hierarchy |
| **Correct Use of try-catch** | 1 | All operations wrapped in proper try-catch |
| **Validation & Error Triggers** | 1 | Input validation before every operation |
| **Clarity of Error Messages** | 0.5 | Clear messages with error codes |
| **Choice of Data Structures** | 1 | HashMap for fast lookup and ArrayList for ordered data |
| **Data Integrity** | 2 | No duplicates and consistent state enforcement |
| **Operations on Collections** | 1 | Filter, search, iterate, add, and remove |
| **Use in Real Context** | 1 | Collections used realistically for academic records |
| **Generic Classes/Methods** | 5 | Repository interface and GenericRepository class |
| **Type Safety** | 5 | Compile-time type checking with no raw types |
| **Wildcard Usage** | 5 | Upper bounded and Lower bounded wildcards |
| **Reusability** | 5 | Same repository works for any entity type |

---

## 👨‍💻 Author

University Course Enrollment System
Developed to demonstrate OOP, Exception Handling, Java Collections, and Generics & Wildcards

---

## 📝 License

This project is for educational purposes only.