# AdvanceRag

A production-grade Retrieval-Augmented Generation (RAG) system featuring enterprise-level authentication, semantic search, and an interactive modern interface. Built to demonstrate advanced AI integration with secure, scalable architecture.

---

## Overview

AdvanceRag implements a complete RAG pipeline that enables intelligent question-answering from PDF documents using state-of-the-art language models. The system leverages semantic embeddings for accurate information retrieval and Google's Gemini AI for context-aware response generation.

### Key Features

- **Semantic Search Engine** → Vector embeddings with SentenceTransformers for precise document retrieval
- **AI-Powered Responses** → Google Gemini integration for contextual answer generation
- **Enterprise Authentication** → JWT-based secure authentication with Spring Security
- **Real-time Processing** → Async FastAPI backend for high-performance operations
- **Persistent Storage** → Embedding caching system for optimized performance
- **Modern UI/UX** → Smooth animations with GSAP and Lenis scroll library

---

## Architecture

### System Design

```
Frontend (React + Vite)
        ↓
Auth Backend (Spring Boot) → PostgreSQL
        ↓
RAG Backend (FastAPI) → Gemini AI
        ↓
Vector Store (NumPy) → PDF Processing
```

### Technology Stack

**RAG Backend (Python)**
- **FastAPI** → High-performance async web framework
- **SentenceTransformers** → State-of-the-art semantic embeddings
- **PyMuPDF** → Efficient PDF parsing and text extraction
- **Google Generative AI** → Gemini model integration
- **NumPy** → Vector storage and similarity computation
- **CORS Middleware** → Cross-origin resource sharing

**Authentication Backend (Java)**
- **Spring Boot** → Enterprise-grade Java framework
- **Spring Security** → Comprehensive security architecture
- **JWT (JSON Web Tokens)** → Stateless authentication mechanism
- **PostgreSQL** → Relational database for user management
- **BCrypt** → Password hashing algorithm

**Frontend (JavaScript)**
- **React** → Component-based UI library
- **Vite** → Next-generation build tool
- **Tailwind CSS v4** → Utility-first styling framework
- **GSAP (GreenSock)** → Professional-grade animations
- **Lenis** → Smooth scroll implementation
- **Axios** → HTTP client for API communication

---

## How It Works

### RAG Pipeline

1. **Document Ingestion** → PDF is downloaded and parsed into text chunks
2. **Vectorization** → Text chunks are converted to semantic embeddings using SentenceTransformers
3. **Storage** → Embeddings are cached in NumPy format for fast retrieval
4. **Query Processing** → User queries are embedded using the same model
5. **Similarity Search** → Cosine similarity identifies the most relevant document chunks
6. **Context Building** → Top-k relevant chunks are selected as context
7. **Generation** → Gemini AI generates responses based on retrieved context

### Authentication Flow

1. **Registration** → User credentials are hashed with BCrypt and stored in PostgreSQL
2. **Login** → Credentials are verified and JWT token is issued
3. **Authorization** → JWT token is validated on each request to protected endpoints
4. **Session Management** → Token expiration and refresh mechanism

---

## Installation & Setup

### Prerequisites

- Python 3.8+
- Java 21+
- Maven
- Node.js 16+
- PostgreSQL 13+
- Google Gemini API Key

### 1. Database Configuration

Create PostgreSQL database:

```sql
CREATE DATABASE elrond;
CREATE USER uday WITH PASSWORD 'Uday@88717';
GRANT ALL PRIVILEGES ON DATABASE elrond TO uday;
```

Or update `sec/src/main/resources/application.properties` with your credentials:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/your_db
spring.datasource.username=your_user
spring.datasource.password=your_password
```

### 2. RAG Backend Setup (Port 8000)

Create virtual environment:

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1  # Windows
# source .venv/bin/activate   # Linux/Mac
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Configure environment variables:

```bash
$env:GOOGLE_API_KEY = "your-gemini-api-key-here"

# Optional: Match JWT secret with Spring Boot
$env:JWT_SECRET = "your-secret-key"
```

Start the server:

```bash
uvicorn src.app:app --reload --port 8000
```

The RAG backend will:
- Automatically download `human-nutrition-text.pdf`
- Generate embeddings on first run
- Cache embeddings in `src/embeddings.npz` for subsequent runs

### 3. Authentication Backend Setup (Port 8080)

Navigate to the Spring Boot directory:

```bash
cd sec
```

Run with Maven wrapper:

```bash
./mvnw spring-boot:run  # Linux/Mac
# mvnw.cmd spring-boot:run  # Windows
```

The authentication server provides:
- User registration endpoint
- Login with JWT token generation
- Protected routes validation
- User management

### 4. Frontend Setup (Port 5173)

Navigate to frontend directory:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start development server:

```bash
npm run dev
```

---

## Usage

### Accessing the Application

1. Open browser and navigate to `http://localhost:5173`
2. You'll be redirected to the login page
3. Click "Register" to create a new account
4. After registration, login with your credentials
5. Access the RAG interface to ask questions about the PDF content

### API Endpoints

**RAG Backend (Port 8000)**
```
POST /query → Submit question and receive AI-generated answer
GET /health → Check backend status
```

**Auth Backend (Port 8080)**
```
POST /api/auth/register → Create new user account
POST /api/auth/login → Authenticate and receive JWT token
GET /api/auth/validate → Validate JWT token
```

---

## Project Structure

```
AdvanceRag/
├── src/
│   ├── app.py              # FastAPI application
│   ├── embeddings.npz      # Cached vector embeddings
│   └── human-nutrition-text.pdf
├── sec/
│   ├── src/main/
│   │   ├── java/           # Spring Boot source
│   │   └── resources/      # Configuration files
│   └── pom.xml             # Maven dependencies
├── frontend/
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── pages/          # Page components
│   │   └── utils/          # Utility functions
│   └── package.json
└── requirements.txt        # Python dependencies
```

---

## Performance Optimizations

- **Embedding Cache** → Avoids recomputing embeddings on every startup
- **Async Operations** → Non-blocking I/O for concurrent request handling
- **Vector Similarity** → Efficient NumPy operations for fast retrieval
- **Connection Pooling** → Optimized database connections
- **Lazy Loading** → Frontend components load on demand

---

## Security Features

- **Password Hashing** → BCrypt algorithm with salt
- **JWT Authentication** → Stateless token-based auth
- **CORS Configuration** → Controlled cross-origin access
- **SQL Injection Prevention** → Parameterized queries
- **XSS Protection** → React's built-in sanitization

---

## Future Enhancements

- Multi-document support
- Custom model fine-tuning
- Conversation history
- Advanced chunking strategies
- Real-time collaboration
- Docker containerization
- Cloud deployment

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## License

This project is open source and available under the MIT License.

---

## Acknowledgments

**Project Contributors**

[@Surendra1341](https://github.com/Surendra1341) · Lead Developer  
[@UdayKhare09](https://github.com/UdayKhare09) · Backend Architecture & Authentication

Built with ❤️ using cutting-edge AI and web technologies
