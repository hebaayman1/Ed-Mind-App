# Development Sprints: AI Study Assistant

This document outlines the agile development sprints for the AI Study Assistant (Version 1.0).

## Sprint 1: Authentication Module & Foundation
**Goal:** Set up the core project repositories, database connection, and a complete, secure user authentication module.

* **Backend Tasks (Flask & PostgreSQL):**
  * Initialize Flask project and configure SQLAlchemy as the ORM.
  * Create the `Users` database table with the exact fields: `id`, `username`, `email`, `password_hash`, and `created_at`.
  * Build the API endpoints for the Authentication Module: Register an account, Log in, and Log out.
  * Implement strict security requirements: passwords must be hashed before storage, and user data must be isolated.
  * Ensure that only authenticated users may access study materials through secure API routing.
  * *(Note: Password reset is marked as a future enhancement and will be skipped for Version 1.0).*
* **Frontend Tasks (Next.js):**
  * Initialize Next.js project.
  * Build the User Authentication UI: Login page and Registration page.
  * Implement authentication state management (e.g., storing the JWT/session token securely) so the frontend knows if a user is logged in.
  * Protect frontend routes so unauthenticated users are redirected to the login page.

## Sprint 2: Core Data (Subjects, Lectures, & Extraction)
**Goal:** Allow users to organize their study materials and extract text from uploaded PDFs.

* **Backend Tasks:**
  * Create the `Subjects` and `Lectures` database tables, linked via foreign keys.
  * Build API endpoints for Subject Management: Create, edit, delete, and view all subjects.
  * Build API endpoints for Lecture Management: Upload PDF, paste text, enter a title, delete, and view history.
  * Integrate `pdfplumber` and `PyPDF2` to extract text from standard PDFs in under 10 seconds.
  * Store the extracted text in the database and allow users to edit it before AI processing.
* **Frontend Tasks:**
  * Build Subject management screens (CRUD operations).
  * Build the Lecture creation interface (File upload for PDF, text area for pasted notes).
  * Build a view to display and edit extracted lecture text.

## Sprint 3: AI Integration - Summaries & Flashcards
**Goal:** Connect the AI model to generate foundational study materials.

* **Backend Tasks:**
  * Create the `Summaries` and `Flashcards` database tables.
  * Integrate the AI Service (Groq/OpenAI compatible LLM) into the Flask backend.
  * Write system prompts to generate short summaries, detailed summaries, key points, and important concepts.
  * Write system prompts to generate double-sided flashcards (Front and Back).
  * Save the AI-generated responses to the PostgreSQL database.
* **Frontend Tasks:**
  * Add UI triggers to generate summaries and flashcards on a lecture page.
  * Build the UI to display Summaries nicely formatted.
  * Build an interactive Flashcard component for studying.

## Sprint 4: Advanced AI Features - Quizzes & Study Plans
**Goal:** Expand AI capabilities to generate interactive MCQs and personalized schedules.

* **Backend Tasks:**
  * Create the `MCQs` and `StudyPlans` database tables.
  * Write API logic to generate Multiple Choice Questions, including four options, the correct answer, and an explanation.
  * Allow users to request exactly 5, 10, or 20 questions.
  * Write API logic to generate daily study schedules, topic orders, recommended hours, and revision sessions based on an exam date.
* **Frontend Tasks:**
  * Build the Quiz UI allowing users to select their desired number of questions and interactive answering logic.
  * Build the Study Plan UI to take an exam date as input and display the generated daily schedule.

## Sprint 5: Dashboard, Polish, & Deployment
**Goal:** Tie everything together with a comprehensive dashboard, refine the UI, and deploy the application.

* **Backend & Frontend Tasks:**
  * Build the Dashboard to display aggregate stats: total subjects, total lectures, total summaries, total flashcards, total quizzes, and recently uploaded lectures.
  * Ensure the UI is responsive, clean, and simple, with easy navigation.
  * Implement automatic database transactions, error handling for failed AI requests, and file validation before uploads.
  * Verify overall response times are under 5 seconds (excluding AI generation time).
  * Deploy Frontend, Backend API, and PostgreSQL Database to your chosen free hosts.
