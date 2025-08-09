
# MCP Starter for Puch AI

This is a starter template for building your own Model Context Protocol (MCP) server to extend Puch AI with custom tools. It includes ready-made tools for job searching, image processing, and interview coaching powered by OpenAI.

---

## What is MCP?

MCP (Model Context Protocol) is a secure way for AI assistants like Puch AI to connect with external tools and APIs, enabling extended capabilities while maintaining security and control.

---

## Included Tools

### 🎯 Job Finder
- Analyze job descriptions
- Extract job posting details from URLs
- Search for relevant jobs using natural language

### 🖼️ Image Processing
- Convert uploaded images to black & white

### 🧑‍💼 Interview Coach (New!)
- Analyze your resume, job description, and interview answers
- Receive AI-powered feedback on improving your resume and interview responses
- Get tailored tips to boost your interview performance

---

## Getting Started

### Prerequisites

- Python 3.11 or newer
- An OpenAI API key (for the interview coach tool)

### Setup

1. **Clone the repository and create a virtual environment**

   ```bash
   git clone <repo-url>
   cd mcp-starter
   uv venv
   uv sync
   source .venv/bin/activate
   ```

2. **Configure environment variables**

   Copy `.env.example` to `.env` and update:

   ```env
   AUTH_TOKEN=your_secret_auth_token
   MY_NUMBER=919876543210
   OPENAI_API_KEY=your_openai_api_key_here
   ```

   - `AUTH_TOKEN`: Secret token for API authentication
   - `MY_NUMBER`: Your WhatsApp number in international format (e.g., `919876543210`)
   - `OPENAI_API_KEY`: OpenAI key for the interview coach tool

3. **Run the server**

   ```bash
   python mcp_starter.py
   ```

   Server will start on `http://0.0.0.0:8086`

---

## Exposing Your Server Publicly

Puch AI requires an HTTPS accessible endpoint.

### Option 1: Using ngrok (Recommended)

- Download and install ngrok: https://ngrok.com/download
- Authenticate ngrok:

  ```bash
  ngrok config add-authtoken YOUR_NGROK_AUTHTOKEN
  ```

- Start ngrok tunnel:

  ```bash
  ngrok http 8086
  ```

- Use the displayed HTTPS URL to connect with Puch AI.

### Option 2: Deploy to Cloud

Deploy on platforms like Railway, Render, Heroku, or DigitalOcean.

---

## Connecting with Puch AI

1. Open a conversation with Puch AI: [https://wa.me/+919998881729](https://wa.me/+919998881729)
2. Use the connect command:

   ```
   /mcp connect https://your-ngrok-or-cloud-url/mcp your_secret_auth_token
   ```

3. For verbose diagnostics:

   ```
   /mcp diagnostics-level debug
   ```

---

## Interview Coach Tool Details

This tool uses OpenAI's GPT-4o-mini model to analyze your resume, job description, and interview answer, then provides personalized feedback and improvement suggestions.

### Inputs

| Parameter         | Description                       |
|-------------------|---------------------------------|
| `resume_text`     | Your resume as plain text        |
| `job_description` | Job description you’re applying for |
| `interview_answer`| Your answer to an interview question |

### Output

- Resume improvement suggestions tailored to the job
- Constructive feedback on your interview answer
- Practical interview performance tips

### Example Usage

```python
response = interview_coach(
    resume_text="Experienced Java developer with 5 years...",
    job_description="Looking for a full-stack developer proficient in Java and React...",
    interview_answer="My greatest strength is problem-solving and teamwork..."
)
print(response.text)
```

---

## Adding Your Own Tools

Add new tools by defining async functions decorated with `@mcp.tool`:

```python
@mcp.tool(description="Your tool description here")
async def your_tool_name(
    param: Annotated[str, Field(description="Describe parameter")]
) -> str:
    # Your implementation here
    return "Result"
```

---

## Resources and Help

- **Official MCP Documentation:** https://puch.ai/mcp  
- **JSON-RPC 2.0 Spec:** https://www.jsonrpc.org/specification
- **Puch AI Discord:** https://discord.gg/VMCnMvYx
- **Contact Puch AI:** +91 99988 81729 (WhatsApp)

---

**Happy coding! 🚀**  
Use hashtag `#BuildWithPuch` when sharing your MCP projects.

---
