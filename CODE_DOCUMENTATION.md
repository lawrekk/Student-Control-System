# Technical Code Documentation

## 1. Introduction
This document provides a detailed technical overview of the **University Course Management System**. It is intended for developers and technical stakeholders who wish to understand the internal architecture, database design, and code structure of the application.

## 2. System Architecture

### 2.1 Overview
The application follows the standard **Model-View-Controller (MVC)** architectural pattern provided by the Laravel framework. This ensures a clean separation of concerns:
-   **Models**: Handle database interactions and business logic.
-   **Views**: Render the user interface using Blade templates.
-   **Controllers**: Manage incoming HTTP requests, invoke models, and return views.

### 2.2 Technology Stack
-   **Framework**: Laravel 12.x
-   **Language**: PHP 8.2+
-   **Database**: SQLite (Development), MySQL (Production)
-   **Frontend**: Bootstrap 5, Blade Templating
-   **Server**: Apache/Nginx (via PHP built-in server for dev)

## 3. Database Design

The database schema is designed to support a multi-role educational environment. Below are the key entities and their relationships.

### 3.1 Core Tables

#### `users`
Stores all system users.
-   `id`: Primary Key
-   `name`: User's full name
-   `email`: Unique email address
-   `password`: Hashed password
-   `role`: Enum (`professor`, `student`, `admin`) - *Crucial for authorization*
-   `created_at`, `updated_at`: Timestamps

#### `courses`
Represents an academic course.
-   `id`: Primary Key
-   `instructor_id`: Foreign Key (`users.id`)
-   `code`: Unique course code (e.g., "CS101")
-   `title`: Course name
-   `description`: Course details
-   `credits`: Credit value

#### `course_enrollments`
Pivot table for Student-Course many-to-many relationship.
-   `id`: Primary Key
-   `student_id`: Foreign Key (`users.id`)
-   `course_id`: Foreign Key (`courses.id`)
-   `enrolled_at`: Timestamp

#### `class_schedules`
Manages the weekly timetable.
-   `id`: Primary Key
-   `course_title`: Name of the course
-   `day_of_week`: Day (Monday-Friday)
-   `start_time`, `end_time`: Time slots
-   `room`: Physical location
-   `color_code`: UI color preference

### 3.2 Entity-Relationship Diagram (Textual)
-   **User (Professor)** `1` -- `N` **Course**
-   **User (Student)** `M` -- `N` **Course** (via `course_enrollments`)
-   **Course** `1` -- `N` **Module**
-   **Module** `1` -- `N` **Lesson**
-   **Course** `1` -- `N` **Assignment**
-   **Assignment** `1` -- `N` **Submission**

## 4. Key Components

### 4.1 Controllers (`app/Http/Controllers`)

#### `DashboardController`
-   **Role**: Central hub for redirecting users after login.
-   **Logic**: Checks `Auth::user()->role` and directs to either `dashboard.professor` or `dashboard.student`.

#### `CourseController`
-   **Role**: Manages CRUD operations for courses.
-   **Methods**:
    -   `index()`: Lists courses (filtered by instructor for professors).
    -   `store()`: Validates and saves new course data.
    -   `show()`: Displays course details, modules, and lessons.

#### `ScheduleController`
-   **Role**: Handles the display of the weekly timetable.
-   **Logic**: Fetches `class_schedules` records and formats them for the frontend calendar view.

### 4.2 Models (`app/Models`)

#### `User`
-   **Traits**: `HasApiTokens`, `HasFactory`, `Notifiable`.
-   **Methods**:
    -   `courses()`: Relationship to courses (as student via enrollment).
    -   `taughtCourses()`: Relationship to courses (as instructor).
    -   `isProfessor()`, `isStudent()`: Helper booleans.

#### `Course`
-   **Relationships**: `instructor()`, `students()`, `modules()`, `assignments()`.

### 4.3 Middleware (`app/Http/Middleware`)

#### `auth`
Standard Laravel authentication middleware.

#### Role-Based Guards
The application uses custom guards defined in `config/auth.php` (though primarily logic is handled via role checks in controllers/middleware) to ensure students cannot access professor-only routes.

## 5. Frontend Architecture

### 5.1 Blade Templates (`resources/views`)
-   **Layouts**:
    -   `layouts/app.blade.php`: Main authenticated layout with navigation.
    -   `layouts/guest.blade.php`: Layout for login/register pages.
-   **Components**: Reusable UI elements (buttons, inputs, cards) located in `resources/views/components`.

### 5.2 Styling
-   **Bootstrap 5**: Loaded via CDN in the main layout file.
-   **Custom CSS**: Minimal custom styles applied via inline blocks or `public/css` for specific overrides (e.g., sidebar transitions).

## 6. Security Measures

-   **CSRF Protection**: All `POST`, `PUT`, `DELETE` requests are protected by Laravel's CSRF token verification.
-   **Input Validation**: `FormRequest` classes (e.g., `StoreCourseRequest`) are used to validate user input before processing.
-   **Authorization**: Laravel Policies (to be implemented fully) and Gate checks ensure users can only interact with their own data.
-   **Password Hashing**: Bcrypt is used for secure password storage.

## 7. Directory Structure Highlights

```
app/
├── Http/
│   ├── Controllers/    # Request Handlers
│   ├── Middleware/     # Request Filters
├── Models/             # Database Entities
database/
├── migrations/         # Schema Definitions
├── seeders/            # Fake Data Generators
resources/
├── views/              # HTML Templates
routes/
├── web.php             # Route Definitions
```
