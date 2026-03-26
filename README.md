<div align="center">

# 🎓 University Course Management System

[![Laravel](https://img.shields.io/badge/Laravel-12.x-FF2D20?style=for-the-badge&logo=laravel)](https://laravel.com)
[![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=for-the-badge&logo=php)](https://www.php.net)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3?style=for-the-badge&logo=bootstrap)](https://getbootstrap.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

**A comprehensive, multi-role academic platform for seamless interaction between professors and students.**

[Features](#-features) • [Screenshots](#-screenshots) • [Installation](#-installation-guide) • [Docs](#-database-schema)

</div>

---

## 📖 Project Overview

The **University Course Management System** is a modern, robust web application designed to digitize and streamline the academic experience. It serves as a centralized hub where **Professors** can manage their curriculum and **Students** can track their academic journey.

Built with a focus on **usability**, **performance**, and **security**, the platform eliminates administrative friction, allowing users to focus on what matters most: education.

### 🚀 Key Highlights
*   **Role-Based Access Control**: Distinct, secure environments for Professors and Students.
*   **Dynamic Scheduling**: Interactive class timetables.
*   **Content Management**: Full suite of tools for course creation, assignments, and resource sharing.

---

## ✨ Features

### 🔐 Authentication & Security
*   **Multi-Guard System**: Dedicated authentication guards for `professor` and `student` roles ensure strict data separation.
*   **Secure Registration**: Streamlined onboarding process for new users.

### 👨‍🏫 For Professors
*   **Dashboard Command Center**: Real-time overview of active courses, student enrollment stats, and pending grading tasks.
*   **Course Management**: Create and configure courses with detailed metadata (credits, terms, visibility).
*   **Content Delivery**: Structure courses with **Modules** and **Lessons**.
*   **Assessment Tools**: Create assignments, set deadlines, and grade submissions.

### 👨‍🎓 For Students
*   **Personalized Dashboard**: Instant access to enrolled courses and upcoming deadlines.
*   **Progress Tracking**: Monitor assignment status and grades.
*   **Resource Access**: Download course materials and lecture notes.

### 📅 Academic Tools
*   **Interactive Schedule**: Color-coded weekly timetable for managing lectures and labs.
*   **Profile Management**: Self-service account updates.

---

## 📸 Screenshots

### 🏠 Landing & Authentication

<div align="center">
  <img src="screenshots/firstpage.png" alt="Landing Page" width="800"/>
  <p><em>Modern, welcoming landing page</em></p>
</div>

<div align="center">
  <img src="screenshots/loginasastudentorprofessor.png" alt="Role Selection" width="600"/>
  <p><em>Clear role-based login selection</em></p>
</div>

### 📊 Dashboards

<div align="center">
  <img src="screenshots/teachersdashboard.png" alt="Professor Dashboard" width="800"/>
  <p><em>Professor Dashboard: Analytics and Quick Actions</em></p>
</div>

<div align="center">
  <img src="screenshots/studentdashboard.png" alt="Student Dashboard" width="800"/>
  <p><em>Student Dashboard: Enrolled Courses and Deadlines</em></p>
</div>

### 🛠️ Course Management

<div align="center">
  <img src="screenshots/coursecreationpage.png" alt="Course Creation" width="800"/>
  <p><em>Intuitive Course Creation Interface</em></p>
</div>

<div align="center">
  <img src="screenshots/schedulepage.png" alt="Class Schedule" width="800"/>
  <p><em>Interactive Weekly Class Schedule</em></p>
</div>

---

## 🛠️ Tech Stack

This project leverages a modern, industry-standard stack to ensure reliability and scalability.

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Backend** | **Laravel 12.x** | Robust PHP framework for secure API and logic. |
| **Language** | **PHP 8.2+** | High-performance server-side scripting. |
| **Frontend** | **Bootstrap 5** | Responsive, mobile-first UI framework. |
| **Templating** | **Blade** | Powerful, component-based view engine. |
| **Database** | **SQLite / MySQL** | Flexible data storage (SQLite for dev, MySQL for prod). |
| **Scripting** | **Vanilla JS** | Lightweight client-side interactivity. |

---

## 📥 Installation Guide

Follow these steps to get a local copy up and running.

### Prerequisites
*   **PHP** >= 8.2
*   **Composer**
*   **Git**

### 1. Clone the Repository
```bash
git clone https://github.com/Ashawn0/student-management-system.git
cd student-management-system
```

### 2. Install Dependencies
```bash
composer install
```

### 3. Configure Environment
```bash
cp .env.example .env
```
*Edit `.env` to configure your database settings if not using the default SQLite.*

### 4. Generate Key
```bash
php artisan key:generate
```

### 5. Setup Database
```bash
# Create SQLite database (Windows PowerShell)
if (!(Test-Path database/database.sqlite)) { New-Item -ItemType File database/database.sqlite }

# Run migrations and seeders
php artisan migrate --seed
```

### 6. Launch Application
```bash
php artisan serve
```
Visit `http://localhost:8000` in your browser.

> **Default Credentials (if seeded):**
> *   **Professor**: `professor@example.com` / `password`
> *   **Student**: `student@example.com` / `password`

---

## 🗄️ Database Schema

The database schema is normalized to handle complex academic relationships efficiently.

### Core Tables
*   **`users`**: Unified user table with `role` discrimination.
*   **`courses`**: Stores course details, linked to an instructor.
*   **`course_enrollments`**: Many-to-Many pivot between Students and Courses.
*   **`class_schedules`**: Stores timetable slots with day/time/room data.
*   **`assignments`**: Assessment tasks linked to courses.
*   **`submissions`**: Student work linked to assignments.

---

## 📂 Folder Structure

```text
laravel-course-system/
├── app/
│   ├── Http/Controllers/    # Application Logic
│   ├── Models/              # Eloquent ORM Models
│   └── View/Components/     # Blade Components
├── database/
│   ├── migrations/          # Schema Definitions
│   └── seeders/             # Dummy Data Generators
├── public/
│   └── screenshots/         # Project Images
├── resources/
│   └── views/               # UI Templates
└── routes/
    └── web.php              # Route Definitions
```

---

## 🔮 Future Improvements

*   [ ] **Real-time Chat**: WebSocket-powered messaging between students and professors.
*   [ ] **Attendance System**: QR code-based attendance tracking.
*   [ ] **Gradebook Export**: PDF/Excel export for course grades.
*   [ ] **Dark Mode**: System-wide dark theme support.

---

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 👥 Credits

**Lead Developer**: AABHUSHAN GYAWALI

Special thanks to the Laravel and Bootstrap communities for their excellent documentation and resources.

<div align="center">

**Built with ❤️ for Education**

</div>
