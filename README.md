# Excel AI Chatbot

An AI chatbot powered by **Claude** that uses an **Excel file** as its database — storing chat history and a knowledge base.

---

## Project Structure

```
├── backend/
│   ├── main.py           # FastAPI application
│   └── requirements.txt  # Python dependencies
├── frontend/
│   └── index.html        # Chat UI (open in browser)
└── chatbot_data.xlsx     # Auto-created on first run
```

---

## Setup & Run

### 1. Install Python dependencies

```bash
cd backend
pip install -r requirements.txt
```

### 2. Set your Anthropic API key

```bash
# macOS / Linux
export ANTHROPIC_API_KEY=your_api_key_here


# Windows (Command Prompt)
set ANTHROPIC_API_KEY=your_api_key_here

# Windows (PowerShell)
$env:ANTHROPIC_API_KEY=your_api_key_here

```

Get your key at: https://console.anthropic.com

### 3. Start the backend

```bash
cd backend
uvicorn main:app --reload --port 8000
```

The API will be available at `http://localhost:8000`

### 4. Open the frontend

Simply open `frontend/index.html` in your browser — no server needed.

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/chat` | Send a message, get AI reply |
| GET | `/history/{session_id}` | Get chat history for a session |
| GET | `/knowledge` | List all knowledge base entries |
| POST | `/knowledge` | Add a new knowledge base entry |
| DELETE | `/knowledge/{topic}` | Delete a knowledge base entry |
| GET | `/sessions` | List all session IDs |

### Example: Send a chat message

```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"session_id": "user123", "message": "What are your support hours?"}'
```

---

## Excel File Structure

The `chatbot_data.xlsx` file is auto-created with two sheets:

**ChatHistory** — every message saved here:
| id | session_id | role | message | timestamp |
|----|------------|------|---------|-----------|

**KnowledgeBase** — context the AI uses to answer questions:
| topic | content |
|-------|---------|

You can edit the Excel file directly to bulk-add knowledge base entries!

---

## Interactive API Docs

FastAPI auto-generates docs at: `http://localhost:8000/docs`
