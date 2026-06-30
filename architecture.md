# Architecture Overview: AI Study Assistant

## 1. System Overview
The AI Study Assistant is a web-based application designed to help students optimize their study time using artificial intelligence. The system allows users to upload lecture materials (PDFs) or input text, which is then processed by an AI engine to generate study aids like summaries, flashcards, multiple-choice questions (MCQs), and personalized study plans.

## 2. Technology Stack
This project uses a decoupled client-server architecture to ensure scalability and ease of deployment.

### Frontend (Client)
* **Framework:** Next.js (React)
* **Styling:** Tailwind CSS
* **Role:** Handles the User Interface (UI), routing, state management, and user interactions. Displays the dashboard, lecture management screens, and the generated AI study materials.

### Backend (API Server)
* **Framework:** Flask (Python)
* **Authentication:** Flask-Login or JWT-based authentication
* **PDF Processing:** `pdfplumber` and `PyPDF2`
* **Role:** Acts as the central API. It handles user authentication, manages file uploads, extracts text from standard PDFs (within 10 seconds), communicates with the AI service, and performs all database operations.

### Database
* **Database Management System:** PostgreSQL
* **ORM:** SQLAlchemy
* **Role:** Persistently stores user accounts, subjects, lecture content, and all AI-generated study materials for future review.

### AI Service
* **Provider:** Groq API (High-speed LLM compatible with OpenAI standards)
* **Role:** Analyzes extracted lecture text to generate short and detailed summaries, key concepts, MCQs (5, 10, or 20 questions), double-sided flashcards, and personalized daily study schedules based on exam dates.

## 3. Data Flow
1. **User Input:** The user logs in and uploads a PDF lecture or pastes text into the Next.js frontend.
2. **API Request:** The frontend sends the file/text via a POST request to the Flask backend.
3. **Processing:** 
   - If a PDF is uploaded, Flask uses `pdfplumber`/`PyPDF2` to extract the text.
   - Flask securely sends the extracted text and a specific prompt to the **Groq API**.
4. **AI Generation:** Groq processes the text and returns structured data (Summaries, MCQs, Flashcards, Study Plan).
5. **Storage:** Flask parses the AI response and saves the data into the **PostgreSQL** database using SQLAlchemy.
6. **Client Update:** Flask returns a success response and the generated data to the Next.js frontend, which renders it for the user.

## 4. Database Schema
The PostgreSQL database consists of 7 core tables:

1. **Users:** `id`, `username`, `email`, `password_hash`, `created_at`
2. **Subjects:** `id`, `user_id` (FK), `name`, `created_at`
3. **Lectures:** `id`, `subject_id` (FK), `title`, `lecture_text`, `pdf_path`, `created_at`
4. **Summaries:** `id`, `lecture_id` (FK), `short_summary`, `detailed_summary`, `key_points`
5. **MCQs:** `id`, `lecture_id` (FK), `question`, `option_a`, `option_b`, `option_c`, `option_d`, `correct_answer`, `explanation`
6. **Flashcards:** `id`, `lecture_id` (FK), `front`, `back`
7. **StudyPlans:** `id`, `lecture_id` (FK), `exam_date`, `generated_plan`

## 5. Deployment & Hosting Strategy (Free Tier)
To maintain a $0 hosting cost while retaining high performance:
* **Frontend Hosting (Next.js):** Vercel or Netlify.
* **Backend Hosting (Flask):** Render, Railway, or PythonAnywhere.
* **Database Hosting (PostgreSQL):** Supabase, Neon, or Render's PostgreSQL tier.
* **Storage (PDFs):** AWS S3 (Free Tier) or Cloudinary for storing uploaded `pdf_path` files.

## 6. Security & Performance Considerations
* All user passwords must be hashed before storage.
* User data must be isolated so authenticated users only access their own study materials.
* The system is designed with automatic database transactions to ensure reliability.
* Non-AI response times should be kept under 5 seconds.