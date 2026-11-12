# SM Company (OMNA People) — AI Recruitment & HR Automation Platform

An end-to-end, self-hosted AI recruitment and HR operations system powered by **n8n**, **Docker**, **Google Workspace**, **Google Gemini**, and **Groq**, paired with a live interactive web portal hosted on GitHub Pages.

🔗 **Live Portal:** [https://mostafaabdelmobdy.github.io/SM-Company-Ai-recruitment-/](https://mostafaabdelmobdy.github.io/SM-Company-Ai-recruitment-/)

---

## 🏗️ System Architecture

The platform orchestrates **five interconnected n8n workflows** using **Google Sheets** as the central state ledger and **Google Drive** for resume storage:

1. **Candidate Intake (`intake.json`)**
   - **Trigger:** n8n Form Submission
   - **Function:** Validates applicant details, checks Google Sheets for duplicate submissions, uploads PDF resumes to Google Drive, logs candidate records, and displays a confirmation page.
2. **AI Resume Screening (`AI scan.json`)**
   - **Trigger:** Scheduled (Hourly) / Manual
   - **Function:** Fetches unscreened applicants, extracts CV text (with OCR fallback for scanned PDFs), structures candidate profiles via **Gemini** & **Groq**, scores applicants against job criteria using self-correcting output schemas, dispatches interview invitations, and flags borderline cases for HR review.
3. **SmartJob Application Coach (`SmartJob Application Coach.json`)**
   - **Trigger:** n8n Form Submission
   - **Function:** Uses an AI Orchestrator invoking three specialist tools (**CV Matcher**, **Cover Letter Writer**, and **Interview Coach**) to analyze a candidate's CV against a target job description and email a tailored report.
4. **HR Policy RAG Assistant (`Rag.json`)**
   - **Trigger:** Public Chat Webhook + Document Upload Form
   - **Function:** Chunks and embeds HR policy documents into an in-memory vector store (`hr_policies`) using **Gemini Embeddings**, enabling a bilingual (**English & العربية**) conversational assistant with memory.
5. **Global Error Handler (`Error Handling.json`)**
   - **Trigger:** n8n Error Trigger + Scheduled Audits
   - **Function:** Classifies workflow failures, throttles duplicate alerts, detects stuck candidate applications, logs incidents in Google Sheets, and sends HTML digest alerts via Gmail.

---

## ✨ Frontend Portal Features (`index.html`)

- **Live Server Heartbeat:** Pings the active `ngrok` + n8n tunnel on load to display real-time `System Online` / `Tunnel Offline` status.
- **Interactive Workflow Inspector & Pipeline Visualizer:** Animated SVG data-flow diagram and downloadable sanitized `.json` workflow files.
- **Bilingual RAG Chat Interface:** Supports automatic RTL/LTR directionality (`dir="auto"`), Markdown formatting, and quick-prompt chips in English and Arabic.
- **Custom Application & Coaching Portals:** Glassmorphic Dark/Light mode UI with drag-and-drop PDF resume zones and direct n8n form launchers.

---

## 🛠️ Tech Stack

- **Workflow Orchestration:** n8n (Self-hosted on Docker)
- **Tunneling & Exposure:** ngrok
- **LLMs & Embeddings:** Google Gemini (`3.1 Flash-Lite`, `2.5 Flash-Lite`, `Gemini Embeddings`), Groq (`gpt-oss-120b`)
- **Storage & Workspace:** Google Sheets, Google Drive, Gmail
- **Frontend:** HTML5, CSS3 (Custom Properties / Glassmorphism), Vanilla JavaScript

---

## 🚀 Quick Setup (Self-Hosted)

1. **Import Workflows:** Import the 5 `.json` files from this repository into your n8n instance and connect your Google Workspace
