# J.A.R.V.I.S AI

J.A.R.V.I.S is a local FastAPI assistant backend that uses Groq for chat responses, Tavily for realtime web search, and a FAISS vector store for learning data and chat memory.

## Features

- General chat endpoint powered by Groq.
- Realtime chat endpoint with Tavily search.
- Local vector store using FAISS and HuggingFace embeddings.
- Chat history support by session ID.
- FastAPI docs available in the browser.

## Project Structure

```text
jarvis_ai/
  app/
    main.py
    models.py
    services/
    utils/
  database/
    chats_data/
    learning_data/
    vector_store/
  config.py
  requirements.txt
  run.py
```

## Setup

Create and activate a virtual environment:

```powershell
cd D:\gaurang\jarvis_ai
python -m venv .venv
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
pip install -r requirements.txt
```

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

Optional extra Groq keys can be added for fallback and rate-limit handling:

```env
GROQ_API_KEY_2=your_second_groq_api_key_here
GROQ_API_KEY_3=your_third_groq_api_key_here
```

## Run

Start the server:

```powershell
python run.py
```

Open the app in the browser:

```text
http://localhost:8000
```

Open API docs:

```text
http://localhost:8000/docs
```

## API Endpoints

- `GET /` - API overview.
- `GET /health` - Service health status.
- `POST /chat` - General chat without web search.
- `POST /chat/realtime` - Chat with realtime Tavily search.
- `GET /chat/history/{session_id}` - Get saved chat history.

Example chat request:

```json
{
  "message": "Hello Jarvis",
  "session_id": "optional-session-id"
}
```

## Local Data

The app creates local folders inside `database/` for chat history, learning data, and vector indexes. These files can contain personal information and generated indexes, so they are ignored by Git.

## Notes

- Keep `.env` private. Do not commit API keys.
- If you change learning data or chat memory, restart the server so the vector store can rebuild.
- Use `Ctrl + C` in the terminal to stop the server.
