# 🚀 Prepverse.AI – AI-Powered Internship Recommendation & Career Preparation Platform

Prepverse.AI is an AI and Machine Learning-powered platform designed to help students discover relevant internship opportunities under the **PM Internship Scheme**. It analyzes candidates' resumes, skills, educational backgrounds, and preferences to recommend suitable internships through semantic search and intelligent ranking.

Beyond internship discovery, Prepverse.AI provides career preparation tools such as AI-powered mock interviews, quizzes, resume evaluation, and automated internship notifications through WhatsApp and Email.

The platform combines modern web technologies, Large Language Models (LLMs), Natural Language Processing (NLP), semantic embeddings, and machine learning to create a personalized internship discovery and preparation experience.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [How the Internship Recommendation System Works](#-how-the-internship-recommendation-system-works)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation and Setup](#-installation-and-setup)
- [Environment Variables](#-environment-variables)
- [Running the Application](#-running-the-application)
- [AI and ML Components](#-ai-and-ml-components)
- [Notification System](#-notification-system)
- [Security and Authentication](#-security-and-authentication)
- [Supported Languages](#-supported-languages)
- [Future Enhancements](#-future-enhancements)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

Finding internships that match a student's skills, qualifications, and career interests can be challenging. Students often spend significant time searching through opportunities that may not be relevant to their profiles.

Prepverse.AI addresses this problem by using AI and ML techniques to understand candidate profiles and match them with suitable internship opportunities.

The platform follows a multi-service architecture consisting of a React frontend, Node.js backend, Python-based ML recommendation engine, and a dedicated resume parsing service.

### 🎯 Project Objectives

- Simplify internship discovery through personalized recommendations.
- Understand candidate profiles using AI-powered resume parsing.
- Improve internship matching through semantic similarity and intelligent ranking.
- Notify candidates about relevant opportunities through WhatsApp and Email.
- Help students prepare for interviews using AI-powered learning tools.
- Provide an accessible and multilingual experience.

---

## ✨ Key Features

### 1. 🤖 AI-Powered Internship Recommendation

The core feature of Prepverse.AI is its personalized internship recommendation engine.

- Analyzes candidate resumes, skills, education, and preferences.
- Generates semantic embeddings using Sentence Transformers.
- Retrieves relevant internship opportunities based on semantic similarity.
- Uses a Cross-Encoder model to rerank retrieved internships.
- Applies skill-based filtering and hybrid ranking.
- Supports stipend, deadline, and location-based filtering.
- Provides personalized internship recommendations based on candidate profiles.

### 2. 📄 AI-Powered Resume Parsing and Evaluation

Prepverse.AI uses an AI-based resume processing pipeline to convert uploaded resumes into structured candidate information.

- Supports PDF resume uploads.
- Extracts resume text using **PyMuPDF**.
- Uses Google Gemini API and LLM-based processing to extract structured information.
- Identifies candidate skills, education, experience, and other relevant details.
- Generates structured resume profiles for downstream recommendation processing.
- Supports resume evaluation and summarization.

### 3. 🎤 AI-Powered Mock Interviews

The platform provides an AI-assisted interview preparation experience.

- Generates interview questions using LLMs.
- Supports dynamic questions based on candidate information.
- Evaluates candidate responses using AI.
- Uses Ollama for local LLM-based interview processing.
- Integrates MediaPipe for facial detection and interview-related analysis.

### 4. 📝 AI-Powered Quizzes

- Generates quizzes using AI.
- Helps candidates practice technical and conceptual topics.
- Supports personalized preparation through AI-generated questions.

### 5. 📧 Automated Email Notifications

- Sends internship-related notifications through email.
- Uses Nodemailer for email delivery.
- Helps candidates stay informed about relevant internship opportunities.

### 6. 📱 WhatsApp Notifications

- Integrates the Meta WhatsApp Cloud API.
- Sends internship alerts through WhatsApp.
- Provides another channel for candidates to receive relevant opportunity updates.

### 7. 📱 Responsive User Interface

- Built with React.js and Tailwind CSS.
- Provides a mobile-friendly interface.
- Offers a convenient experience across different screen sizes.

---

## 🧠 How the Internship Recommendation System Works

The recommendation engine combines semantic retrieval, skill-based filtering, and Cross-Encoder reranking to identify relevant internship opportunities.

### Recommendation Pipeline

```text
                 Candidate Resume
                        |
                        v
                Resume Upload
                        |
                        v
              Resume Text Extraction
                   (PyMuPDF)
                        |
                        v
              AI Resume Processing
             (Gemini API / LLM)
                        |
                        v
              Structured Candidate
                    Profile
                        |
                        v
              Candidate Embedding
            (BGE Sentence Transformer)
                        |
                        v
             Semantic Retrieval
               (MongoDB Vector Search)
                        |
                        v
               Initial Candidates
                        |
                        v
             Skill-Based Filtering
                        |
                        v
             Cross-Encoder Reranking
                        |
                        v
               Hybrid Ranking
                        |
                        v
             Personalized Internship
                Recommendations
```

### Step 1: Resume Upload and Extraction

The candidate uploads a resume in PDF format through the frontend.

The backend forwards the uploaded document to the Python-based resume parsing service. PyMuPDF extracts the text from the PDF.

### Step 2: AI-Based Resume Processing

The extracted resume content is processed using Google Gemini API and LLM-based functions.

The processing pipeline identifies relevant candidate information and generates a structured resume profile.

### Step 3: Embedding Generation

The recommendation engine uses the **BAAI/bge-large-en-v1.5** Sentence Transformer model to convert candidate information into numerical vector embeddings.

Internship descriptions are also represented using embeddings so that candidate profiles and internship requirements can be compared semantically.

### Step 4: Semantic Retrieval

The generated candidate embedding is used to retrieve semantically relevant internship opportunities from the internship dataset stored in MongoDB.

The retrieval stage identifies potentially suitable opportunities based on the meaning and context of candidate information rather than relying only on exact keyword matches.

### Step 5: Skill-Based Filtering

The retrieved internships are further processed using skill extraction and matching logic.

The engine considers:

- Candidate skills.
- Internship-required skills.
- Skill overlap.
- Candidate preferences.
- Stipend requirements.
- Application deadlines.
- Geographic preferences.

### Step 6: Cross-Encoder Reranking

The retrieved candidate-internship pairs are passed to the **cross-encoder/ms-marco-electra-base** model.

Unlike the initial bi-encoder retrieval stage, the Cross-Encoder evaluates each candidate-internship text pair together to produce a more contextual relevance score.

### Step 7: Hybrid Ranking

The recommendation engine combines semantic relevance with additional matching criteria to rank suitable internships.

Geographic filtering can use Haversine distance calculations, while MongoDB geospatial indexing supports location-based queries.

### Step 8: Personalized Recommendations

The final ranked results are returned to the backend and displayed to the candidate through the React frontend.

---

## 🏗️ System Architecture

Prepverse.AI follows a modular, multi-service architecture. Each service handles a specific responsibility and communicates with the other services through APIs and database operations.

### Main Services

| Service | Technology | Responsibility |
|---|---|---|
| Frontend | React.js, Vite, Tailwind CSS | User interface and candidate interactions |
| Backend | Node.js, Express.js, MongoDB | REST APIs, authentication, data management, and notifications |
| ML Engine | Python, Flask, Sentence Transformers | Semantic retrieval, internship matching, and ranking |
| Client Parser | Python, Flask, PyMuPDF, LLMs | Resume extraction, parsing, evaluation, and summarization |

### Architecture Overview

```text
                   ┌─────────────────────┐
                   │     React Frontend  │
                   │   React + Vite      │
                   └──────────┬──────────┘
                              |
                              v
                   ┌─────────────────────┐
                   │    Node.js Backend  │
                   │  Express + REST API │
                   └──────┬───────┬──────┘
                          |       |
             ┌────────────┘       └────────────┐
             v                                v
  ┌─────────────────────┐          ┌─────────────────────┐
  │    Client Parser    │          │      ML Engine      │
  │   Python + Flask    │          │   Python + Flask    │
  │                     │          │                     │
  │ PyMuPDF             │          │ Sentence Transformers│
  │ Gemini / LLM        │          │ Semantic Retrieval  │
  │ Resume Processing  │          │ Cross-Encoder       │
  └─────────────────────┘          └──────────┬──────────┘
                                              |
                                              v
                                   ┌─────────────────────┐
                                   │      MongoDB        │
                                   │ Candidate & Internship│
                                   │ Data and Embeddings │
                                   └─────────────────────┘
```

---

## 🛠️ Technology Stack

### Frontend

- **React.js** – Component-based user interface.
- **Vite** – Frontend development and build tooling.
- **Tailwind CSS** – Responsive UI styling.

### Backend

- **Node.js** – JavaScript runtime.
- **Express.js** – REST API development.
- **MongoDB** – NoSQL database.
- **Mongoose** – MongoDB object modeling.
- **JWT** – Authentication and authorization.
- **Socket.IO** – Real-time communication support.
- **Cloudinary** – Media and file management.
- **Nodemailer** – Email notifications.
- **Meta WhatsApp Cloud API** – WhatsApp notifications.

### AI and Machine Learning

- **Python** – ML and AI service development.
- **Flask** – Python API services.
- **Sentence Transformers** – Semantic embedding generation.
- **BAAI/bge-large-en-v1.5** – Bi-encoder embedding model.
- **cross-encoder/ms-marco-electra-base** – Cross-Encoder reranking model.
- **Google Gemini API** – LLM-based resume processing.
- **Ollama** – Local LLM inference.
- **MediaPipe** – Facial detection and analysis.
- **PyMuPDF** – PDF text extraction.

### Database and Infrastructure

- **MongoDB Atlas** – Cloud database.
- **MongoDB Vector Search** – Semantic retrieval.
- **MongoDB Geospatial Indexing** – Location-based filtering.
- **Git and GitHub** – Version control and collaboration.

---

## 📁 Project Structure

The project is organized into four main services:

```text
Prepverse.AI/
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── assets/
│   │   └── ...
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   ├── package.json
│   └── ...
│
├── Ml_Engine/
│   ├── app.py
│   ├── recommend_service.py
│   ├── parsingData.py
│   ├── requirements.txt
│   └── ...
│
├── clientParser/
│   ├── app.py
│   ├── requirements.txt
│   └── ...
│
├── .gitignore
└── README.md
```

*Note: This is a high-level representation of the service organization. Individual filenames and subdirectories may differ in your current repository.*

---

## ⚙️ Installation and Setup

Follow these steps to run Prepverse.AI locally.

### Prerequisites

Install the following tools before starting:

- [Node.js](https://nodejs.org/) – Version 18 or later.
- [Python](https://www.python.org/) – Version 3.11 or later.
- [MongoDB Atlas](https://www.mongodb.com/atlas) account or a local MongoDB instance.
- [Ollama](https://ollama.com/) – For local LLM inference.
- [Git](https://git-scm.com/).

### 1. Clone the Repository

```bash
git clone https://github.com/Hrusikesh001/Prepverse.AI.git

cd Prepverse.AI
```

### 2. Setup the Frontend

```bash
cd frontend

npm install
```

Create the required frontend environment file and configure the backend API URL according to your application configuration.

Start the development server:

```bash
npm run dev
```

### 3. Setup the Backend

Open a new terminal:

```bash
cd backend

npm install
```

Configure the backend environment variables in a `.env` file.

Start the backend using the start script defined in `package.json`:

```bash
npm start
```

If your package configuration uses a development script, you can use:

```bash
npm run dev
```

### 4. Setup the ML Engine

Open another terminal:

```bash
cd Ml_Engine
```

Create a Python virtual environment:

```bash
python -m venv venv
```

Activate the environment.

**Windows PowerShell:**

```powershell
.\venv\Scripts\Activate.ps1
```

**Linux / macOS:**

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the Flask ML service using the entry point and run configuration defined in the project.

For example, if `app.py` is configured as the Flask entry point:

```bash
python app.py
```

### 5. Setup the Client Parser

Open another terminal:

```bash
cd clientParser
```

Create and activate a separate Python virtual environment:

```bash
python -m venv venv
```

**Windows PowerShell:**

```powershell
.\venv\Scripts\Activate.ps1
```

**Linux / macOS:**

```bash
source venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Configure the required API credentials and start the Flask application using its configured entry point.

For example:

```bash
python app.py
```

### 6. Setup Ollama Models

Install Ollama and pull the models required by the relevant project features.

For example, the project documentation references these models:

```bash
ollama pull llama3.1:8b
ollama pull llama3.2
ollama pull bge-m3
```

Make sure the required Ollama service is running before using features that depend on local model inference.

*Use the exact model names and versions configured in your current application code.*

---

## 🔐 Environment Variables

Create separate `.env` files for the frontend and backend wherever required by your application.

The following is a configuration reference. Replace the placeholders with your actual credentials and use the exact variable names expected by your source code.

### Backend Environment Variables

```env
PORT=YOUR_BACKEND_PORT

MONGODB_URI=YOUR_MONGODB_CONNECTION_STRING

JWT_SECRET=YOUR_JWT_SECRET

GEMINI_API_KEY=YOUR_GEMINI_API_KEY

CLOUDINARY_CLOUD_NAME=YOUR_CLOUDINARY_CLOUD_NAME
CLOUDINARY_API_KEY=YOUR_CLOUDINARY_API_KEY
CLOUDINARY_API_SECRET=YOUR_CLOUDINARY_API_SECRET

EMAIL_USER=YOUR_EMAIL_ADDRESS
EMAIL_PASS=YOUR_EMAIL_APP_PASSWORD

WHATSAPP_ACCESS_TOKEN=YOUR_WHATSAPP_ACCESS_TOKEN
WHATSAPP_PHONE_NUMBER_ID=YOUR_PHONE_NUMBER_ID
```

### Frontend Environment Variables

```env
VITE_API_URL=YOUR_BACKEND_API_URL
```

### Important Security Notes

- Never commit `.env` files to GitHub.
- Never expose API keys or database credentials in frontend code.
- Use strong JWT secrets.
- Keep WhatsApp, email, Cloudinary, and LLM credentials private.
- Configure the required environment variables separately for development and production.
- Add `.env` files to `.gitignore`.

---

## 🧪 AI and ML Components

### Bi-Encoder Semantic Embeddings

The recommendation engine uses:

```text
BAAI/bge-large-en-v1.5
```

The model converts candidate profiles and internship descriptions into vector representations.

These embeddings allow the system to identify semantic relationships between candidate skills and internship requirements.

### Cross-Encoder Reranking

The project uses:

```text
cross-encoder/ms-marco-electra-base
```

The Cross-Encoder evaluates retrieved candidate-internship pairs together to improve contextual relevance ranking.

### Resume Processing

The resume parsing pipeline combines:

- PDF text extraction using PyMuPDF.
- LLM-based information extraction.
- Structured candidate profile generation.
- Resume evaluation and summarization.

### Local LLM Integration

Ollama is used for local LLM-based functionality, including AI-assisted interview and quiz workflows.

### Geospatial Matching

The recommendation engine includes location-based matching functionality using:

- Haversine distance calculations.
- Geographic filtering.
- MongoDB geospatial indexing.

---

## 🔔 Notification System

Prepverse.AI provides automated notification functionality to help candidates stay informed about relevant internship opportunities.

### Email Notifications

Nodemailer is used to send email notifications through the configured email service.

### WhatsApp Notifications

The Meta WhatsApp Cloud API is integrated to deliver internship-related alerts directly through WhatsApp.

These notification channels help candidates receive relevant updates without repeatedly checking the platform.

---

## 🔒 Security and Authentication

The backend handles authentication and application-level security.

The project includes:

- JWT-based authentication.
- Protected API routes.
- Authentication middleware.
- Password and user credential handling.
- OAuth-based authentication support.
- OTP-based verification functionality.

Sensitive credentials and API tokens are managed through environment configuration rather than being stored in the source code.

---

## 🚧 Future Enhancements

Potential areas for further development include:

- Expanding internship coverage across additional programs and organizations.
- Improving recommendation quality through feedback-based ranking.
- Adding more detailed recommendation explanations.
- Enhancing candidate analytics and application tracking.
- Improving resume evaluation and career guidance.
- Expanding multilingual support.
- Adding more interview practice and assessment features.

---

## 🤝 Contributing

Contributions, suggestions, and feedback are welcome!

To contribute:

1. Fork the repository.
2. Create a new feature branch.

```bash
git checkout -b feature/your-feature-name
```

3. Make your changes.
4. Commit your changes.

```bash
git commit -m "Add: your feature description"
```

5. Push the branch.

```bash
git push origin feature/your-feature-name
```

6. Open a Pull Request describing your changes.

---

## 👨‍💻 Author

**Hrusikesh Sahu**

B.Tech – Computer Science and Engineering
- LinkedIn: [Connect on LinkedIn]([https://www.linkedin.com/](https://www.linkedin.com/in/hrusikesh-sahu-895420300/))

---

## ⭐ Support

If you find Prepverse.AI useful, consider giving the repository a ⭐ on GitHub.

Your support and contributions help improve the platform and make internship discovery more accessible to students.

---

