# 🎓 Classroom Backend Service

A robust, feature-rich RESTful API service built with **Node.js**, **Express.js**, and **MongoDB (Mongoose)** to power a modern School and Classroom Management System. Featuring role-based access control (Admin, Teacher, Student) and AI-powered learning tools integrated with **Google Gemini AI**.

---

## 🚀 Key Features

- **🔐 Multi-Role Authentication & Access Control**
  - Dedicated authentication and management pipelines for **Admins**, **Teachers**, and **Students**.
  - Password hashing using `bcrypt` and secure data validation.

- **🤖 AI-Powered Capabilities (Google Gemini)**
  - **AI Quiz Generation**: Automatically generates questions, options, and explanations from subject topics using Gemini AI (`@google/genai`).
  - **AI Assignment Assistance**: Automated grading insights and feedback generation for student submissions.

- **📝 Quizzes & Assessments**
  - Create and manage timed multiple-choice quizzes per class and subject.
  - Automatic answer grading, score calculation, and performance analytics.
  - Detailed student result history and answer breakdown.

- **📂 Assignment Management**
  - Teachers publish assignments with deadlines and max marks.
  - Students submit assignments online.
  - Grading and feedback workflows for instructors.

- **🔬 Lab Group Collaboration**
  - Group creation, capacity tracking, and student allocation for practical labs and collaborative group projects.

- **📊 Comprehensive Attendance System**
  - Individual student attendance tracking per subject.
  - Bulk class attendance marking for quick roll-calls.
  - Teacher daily attendance recording.

- **🏫 Academic Structure Management**
  - Classes (Sclass) creation and student enrolment.
  - Subject cataloging and assigning subject teachers.
  - Exam marks recording and report generation.

- **📢 Communication & Grievances**
  - School-wide circulars and notice boards.
  - Complaint submission and review pipeline.

---

## 🛠️ Tech Stack

- **Runtime**: [Node.js](https://nodejs.org/) (v16+)
- **Framework**: [Express.js](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) with [Mongoose](https://mongoosejs.com/) ODM
- **AI Integration**: [@google/genai](https://www.npmjs.com/package/@google/genai) (Google Gemini API)
- **Security**: [bcrypt](https://www.npmjs.com/package/bcrypt), [cors](https://www.npmjs.com/package/cors)
- **Environment Management**: [dotenv](https://www.npmjs.com/package/dotenv)

---

## 📁 Project Structure

```text
backend/
├── controllers/
│   ├── admin-controller.js          # Admin registration & management
│   ├── assignment-controller.js     # Assignment creation, submission & grading
│   ├── class-controller.js          # Class (Sclass) CRUD operations
│   ├── complain-controller.js       # Student/Teacher grievance handling
│   ├── labGroup-controller.js       # Lab group creation & student allocation
│   ├── notice-controller.js         # Notice creation & announcement feed
│   ├── quiz-controller.js           # Quiz management & Gemini AI quiz generation
│   ├── student_controller.js        # Student profiles, exams, & attendance
│   ├── subject-controller.js        # Subject creation & teacher assignment
│   └── teacher-controller.js        # Teacher management & attendance
├── models/
│   ├── adminSchema.js
│   ├── assignmentSchema.js
│   ├── assignmentSubmissionSchema.js
│   ├── complainSchema.js
│   ├── labGroupSchema.js
│   ├── noticeSchema.js
│   ├── quizResultSchema.js
│   ├── quizSchema.js
│   ├── sclassSchema.js
│   ├── studentSchema.js
│   ├── subjectSchema.js
│   └── teacherSchema.js
├── routes/
│   └── route.js                     # Central API route definitions
├── .env.example                     # Environment variables template
├── .gitignore                       # Git ignore rules
├── index.js                         # Application entrypoint & server setup
├── package.json
└── README.md
```

---

## ⚙️ Setup and Installation

### 1. Prerequisites
- **Node.js** (v16.x or newer installed)
- **MongoDB** running locally (`mongodb://127.0.0.1:27017`) or a [MongoDB Atlas](https://www.mongodb.com/atlas) cloud URI
- *(Optional)* [Google Gemini API Key](https://aistudio.google.com/) for AI quiz and assignment features

### 2. Clone the Repository
```bash
git clone https://github.com/Yogeshpant942/classroom-backend.git
cd classroom-backend
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Configure Environment Variables
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
Update `.env` with your settings:
```env
PORT=5000
MONGO_URL=mongodb://127.0.0.1:27017/smsproject
SECRET_KEY=your_jwt_secret_key
GEMINI_API_KEY=your_gemini_api_key
```

### 5. Start the Server
For development with auto-reloading (`nodemon`):
```bash
npm start
```
The server will run on `http://localhost:5000` (or your defined `PORT`).

---

## 📡 API Reference Overview

### 🔑 Authentication & Administration
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/AdminReg` | Register a new school admin |
| `POST` | `/AdminLogin` | Login as administrator |
| `GET` | `/Admin/:id` | Fetch administrator profile |

### 👨‍🎓 Student Management
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/StudentReg` | Register a student |
| `POST` | `/StudentLogin` | Student login |
| `GET` | `/Students/:id` | List all students in school |
| `GET` | `/Student/:id` | Get student details |
| `PUT` | `/Student/:id` | Update student profile |
| `DELETE` | `/Student/:id` | Remove a student |
| `PUT` | `/StudentAttendance/:id` | Mark individual student attendance |
| `POST` | `/BulkStudentAttendance` | Bulk class attendance marking |
| `PUT` | `/UpdateExamResult/:id` | Record / update exam scores |

### 👩‍🏫 Teacher Management
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/TeacherReg` | Register a new teacher |
| `POST` | `/TeacherLogin` | Teacher authentication |
| `GET` | `/Teachers/:id` | List teachers in school |
| `GET` | `/Teacher/:id` | Get teacher profile & details |
| `PUT` | `/TeacherSubject` | Assign subject to a teacher |
| `POST` | `/TeacherAttendance/:id` | Record teacher attendance |
| `DELETE` | `/Teacher/:id` | Remove teacher record |

### 🏫 Classes & Subjects
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/SclassCreate` | Create a new class |
| `GET` | `/SclassList/:id` | Get list of classes |
| `GET` | `/Sclass/:id` | Get class details |
| `GET` | `/Sclass/Students/:id` | Get all students in a class |
| `POST` | `/SubjectCreate` | Create a subject for a class |
| `GET` | `/AllSubjects/:id` | List all subjects across school |
| `GET` | `/ClassSubjects/:id` | List subjects for a specific class |

### 🤖 AI & Quizzes
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/QuizCreate` | Create a new quiz |
| `GET` | `/QuizzesClass/:id` | Get all quizzes for a class |
| `GET` | `/Quiz/:id` | Get quiz questions & configuration |
| `POST` | `/QuizSubmit` | Submit quiz answers and auto-grade |
| `POST` | `/QuizGenerateAI` | **AI**: Generate quiz questions automatically via Gemini |
| `GET` | `/QuizResults/:id` | Get analytics and scores for a quiz |
| `GET` | `/StudentQuizResults/:id`| Get quiz results for a specific student |
| `DELETE` | `/Quiz/:id` | Delete a quiz |

### 🔬 Lab Groups
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/LabGroupCreate` | Create a lab group in a class |
| `GET` | `/LabGroupsClass/:id` | Get all lab groups for a class |
| `POST` | `/LabGroupAssign` | Assign student to lab group |
| `POST` | `/LabGroupRemoveStudent` | Remove student from group |
| `GET` | `/StudentLabGroup/:id` | Get student's assigned lab group |
| `DELETE` | `/LabGroup/:id` | Delete a lab group |

### 📚 Assignments
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/AssignmentCreate` | Create a new assignment |
| `GET` | `/AssignmentsClass/:id` | Get all assignments for a class |
| `POST` | `/AssignmentSubmit` | Student submission (with optional AI review) |
| `GET` | `/AssignmentSubmissions/:id`| View submissions for an assignment |
| `PUT` | `/AssignmentGrade` | Grade student submission with marks & feedback |
| `GET` | `/StudentSubmissions/:id` | View all submissions by a student |
| `DELETE` | `/Assignment/:id` | Delete an assignment |

### 📢 Notices & Complaints
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/NoticeCreate` | Publish notice/announcement |
| `GET` | `/NoticeList/:id` | List active notices |
| `DELETE` | `/Notice/:id` | Remove notice |
| `POST` | `/ComplainCreate` | Submit grievance / complaint |
| `GET` | `/ComplainList/:id` | List complaints for review |

---

## 📄 License
This project is open source and available under the [ISC License](LICENSE).
