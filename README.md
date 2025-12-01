# 🚀 Automated Article Analysis Gateway

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.95%2B-green)
![Status](https://img.shields.io/badge/Status-Active-success)

A high-performance, asynchronous API service acting as a secure gateway between frontend applications and **n8n** automation workflows.

## 📖 Overview

Directly exposing automation webhooks (like n8n or Zapier) to client-side applications can lead to security vulnerabilities and lack of validation. This project solves that by introducing a **FastAPI middleware layer**.

It accepts article submission requests, validates the data structure, assigns unique session identifiers, and asynchronously forwards the payload to the n8n processing engine.

### 🏗 Architecture

```mermaid
graph LR
    A[Client / Frontend] -->|POST /submit-article| B(FastAPI Gateway)
    B -->|Validation & Session ID| B
    B -->|Async Request| C[n8n Webhook]
    C -->|AI Processing| D[LLM Analysis]
    B -.->|200 OK| A


✨ Key Features
⚡ Asynchronous I/O: Built with async/await and httpx to handle concurrent requests without blocking.

🛡️ Robust Validation: Uses Pydantic models to ensure email addresses and URLs are valid before processing.

🆔 Session Traceability: Generates a unique UUID (session_id) for every request to track data flow across the entire pipeline.

🔒 Secure Configuration: Manages sensitive webhook endpoints via environment variables.

🛠️ Installation & Setup
1. Clone the repository
Bash

git clone [https://github.com/Dev-Pranto/1st_n8n_backend.git](https://github.com/Dev-Pranto/1st_n8n_backend.git)
cd 1st_n8n_backend
2. Create a Virtual Environment
Bash

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
3. Install Dependencies
Bash

pip install -r requirements.txt
4. Configure Environment Variables
Create a .env file in the root directory:

Code snippet

# Your n8n Webhook URL
N8N_URL=[https://your-n8n-instance.com/webhook/your-uuid](https://your-n8n-instance.com/webhook/your-uuid)
🚀 Usage
Start the Server
Bash

uvicorn main:app --reload
The API will be available at http://localhost:8000.

API Endpoint
POST /submit-article

Request Body:

JSON

{
  "email": "user@example.com",
  "article_url": "[https://medium.com/article-slug](https://medium.com/article-slug)"
}
Success Response:

JSON

{
  "message": "Article submitted for processing",
  "session_id": "550e8400-e29b-41d4-a716-446655440000",
  "status": "success"
}
📂 Project Structure
├── main.py           # Application entry point & logic
├── requirements.txt  # Python dependencies
├── .env              # Environment variables (gitignored)
└── README.md         # Documentation
🔮 Future Improvements
[ ] Dockerize the application for containerized deployment.

[ ] Add Rate Limiting to prevent spam abuse.

[ ] Implement a database log to store request history.

👨‍💻 Author
SK Hamim Ishthiaque Pranto

Portfolio: pranto-ai.xyz

LinkedIn: linkedin.com/in/pranto-ai

Built with ❤️ for the Open Source Community.
