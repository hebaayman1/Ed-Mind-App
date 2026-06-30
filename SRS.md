# Software Requirements Specification (SRS)

# AI Study Assistant

**Version:** 1.0  
**Document Date:** June 2026

---

# 1. Introduction

## 1.1 Purpose

The AI Study Assistant is a web-based application that helps students study more efficiently using Artificial Intelligence.

Users can upload lecture materials (PDF), paste lecture text, or type notes manually. The application analyzes the content using an AI model and generates:

- Lecture summaries
- Multiple Choice Questions (MCQs)
- Flashcards
- Personalized study plans

All generated content is stored in a PostgreSQL database for future review.

---

## 1.2 Scope

The system provides students with AI-powered learning tools that reduce study time and improve knowledge retention.

The application includes:

- User authentication
- Lecture management
- AI-generated learning materials
- Search functionality
- Learning history

---

## 1.3 Intended Audience

This document is intended for:

- Developers
- Project supervisors
- Software testers
- UI/UX designers

---

# 2. Project Objectives

The project aims to:

- Help students understand lectures faster.
- Generate high-quality study materials automatically.
- Improve exam preparation.
- Store study history for future access.
- Provide an organized learning experience.

---

# 3. Target Users

- University students
- High school students
- Self-learners
- Online course participants

---

# 4. Technology Stack

## Backend

- Flask

## Database

- PostgreSQL

## ORM

- SQLAlchemy

## Frontend

-Next JS - Tailwind css

## Authentication

- Flask-Login

## AI Service

- Grok AI

## PDF Processing

- pdfplumber
- PyPDF2

---

# 5. Functional Requirements

## 5.1 User Authentication

The system shall allow users to:

- Register an account
- Log in
- Log out
- Reset password (future enhancement)

---

## 5.2 Dashboard

After logging in, users shall be able to view:

- Total subjects
- Total lectures
- Total summaries
- Total flashcards
- Total quizzes
- Recently uploaded lectures

---

## 5.3 Subject Management

Users shall be able to:

- Create subjects
- Edit subjects
- Delete subjects
- View all subjects

Example:

- Database Systems
- Operating Systems
- Artificial Intelligence

---

## 5.4 Lecture Management

Users shall be able to:

- Upload a PDF lecture
- Paste lecture text
- Enter a lecture title
- Select a subject
- Delete lectures
- View lecture history

---

## 5.5 Text Extraction

The system shall:

- Extract text from uploaded PDF files.
- Store the extracted text in the database.
- Allow users to edit extracted text before AI processing.

---

## 5.6 AI Summary Generation

The AI shall generate:

- Short summary
- Detailed summary
- Key points
- Important concepts

---

## 5.7 AI Quiz Generation

The AI shall generate:

- Multiple Choice Questions

Each question shall include:

- Question
- Four options
- Correct answer
- Explanation

Users can choose:

- 5 Questions
- 10 Questions
- 20 Questions

---

## 5.8 Flashcard Generation

The AI shall create flashcards.

Each flashcard contains:

Front

```
Question or Concept
```

Back

```
Answer or Explanation
```

Example:

Front

```
What is Normalization?
```

Back

```
A database design technique used to reduce redundancy.
```

---

## 5.9 Study Plan Generation

Users enter:

- Exam date

The AI generates:

- Daily study schedule
- Recommended study hours
- Topic order
- Revision sessions

---

## 5.10 Search

Users can search lectures by:

- Subject
- Lecture title
- Keywords

---

## 5.11 Learning History

Users shall be able to:

- View previous lectures
- View generated summaries
- View flashcards
- View quizzes
- Regenerate AI content

---

# 6. Non-Functional Requirements

## Performance

- Response time should be under 5 seconds (excluding AI generation time).
- PDF processing should complete within 10 seconds for standard files.

---

## Security

- Passwords must be hashed.
- User data must be isolated.
- Only authenticated users may access study materials.

---

## Usability

- Responsive UI
- Clean and simple interface
- Easy navigation

---

## Reliability

- Automatic database transactions
- Error handling for failed AI requests
- File validation before upload

---

## Scalability

The system should support:

- Thousands of users
- Large numbers of lectures
- Future AI features

---

# 7. Database Design

## Users

| Field | Type |
|--------|------|
| id | Integer |
| username | String |
| email | String |
| password_hash | String |
| created_at | Timestamp |

---

## Subjects

| Field | Type |
|--------|------|
| id | Integer |
| user_id | FK |
| name | String |
| created_at | Timestamp |

---

## Lectures

| Field | Type |
|--------|------|
| id | Integer |
| subject_id | FK |
| title | String |
| lecture_text | Text |
| pdf_path | String |
| created_at | Timestamp |

---

## Summaries

| Field | Type |
|--------|------|
| id | Integer |
| lecture_id | FK |
| short_summary | Text |
| detailed_summary | Text |
| key_points | Text |

---

## MCQs

| Field | Type |
|--------|------|
| id | Integer |
| lecture_id | FK |
| question | Text |
| option_a | String |
| option_b | String |
| option_c | String |
| option_d | String |
| correct_answer | String |
| explanation | Text |

---

## Flashcards

| Field | Type |
|--------|------|
| id | Integer |
| lecture_id | FK |
| front | Text |
| back | Text |

---

## StudyPlans

| Field | Type |
|--------|------|
| id | Integer |
| lecture_id | FK |
| exam_date | Date |
| generated_plan | Text |

---

# 8. System Workflow

```
User Login
      │
      ▼
Dashboard
      │
      ▼
Create / Select Subject
      │
      ▼
Upload PDF or Paste Text
      │
      ▼
Extract Lecture Text
      │
      ▼
Send Content to AI
      │
      ▼
Generate:
    • Summary
    • MCQs
    • Flashcards
    • Study Plan
      │
      ▼
Store Results in PostgreSQL
      │
      ▼
Display Results to User
```

---

# 9. Future Enhancements

- AI Chat with Lecture
- Voice-based study assistant
- Text-to-Speech summaries
- Speech-to-Text notes
- Spaced Repetition System (SRS)
- Difficulty levels for quizzes
- AI-generated diagrams
- Multi-language support
- Collaborative study groups
- Mobile application
- Calendar integration
- Progress analytics dashboard

---

# 10. Project Scope

### Included

- User authentication
- Subject management
- Lecture management
- PDF upload
- Text extraction
- AI summary generation
- AI quiz generation
- Flashcard generation
- Study plan generation
- Search functionality
- History management
- PostgreSQL database integration

### Excluded (Version 1.0)

- Mobile application
- Offline mode
- Video lecture processing
- OCR for handwritten notes
- Real-time collaboration

---

# 11. Success Criteria

The project is considered successful if a user can:

- Register and log in successfully.
- Create and manage subjects.
- Upload lecture materials.
- Extract lecture text.
- Generate AI summaries.
- Generate MCQs.
- Generate flashcards.
- Generate personalized study plans.
- Save all generated content.
- Search previous lectures.
- Access learning history at any time.

---

# 12. Assumptions and Constraints

## Assumptions

- Users have internet access.
- AI service is available.
- Uploaded PDFs contain readable text.

## Constraints

- AI response time depends on the external API.
- Free AI plans may have usage limits.
- PDF quality affects text extraction accuracy.

---

# 13. Future Version (v2.0)

- AI Tutor Chat
- Smart Revision Scheduling
- Exam Prediction
- Learning Progress Dashboard
- Team Study Spaces
- AI Note Improvement
- AI Concept Maps
- AI Mind Map Generation
- Mobile Application (Flutter)
- Email Notifications
- Reminder System