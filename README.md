MCP Starter for Puch AI
This is a starter template for creating your own Model Context Protocol (MCP) server that works with Puch AI. It comes with ready-to-use tools for job searching, image processing, and interview coaching.

What is MCP?
MCP (Model Context Protocol) allows AI assistants like Puch to connect to external tools and data sources safely. Think of it like giving your AI extra superpowers without compromising security.

What's Included in This Starter?
🎯 Job Finder Tool
Analyze job descriptions - Paste any job description and get smart insights

Fetch job postings from URLs - Give a job posting link and get the full details

Search for jobs - Use natural language to find relevant job opportunities

🖼️ Image Processing Tool
Convert images to black & white - Upload any image and get a monochrome version

🧑‍💼 Interview Coach Tool
Analyze your resume, job description, and interview answers

Get AI-powered feedback on how to improve your resume and interview performance

Receive detailed suggestions and tips tailored to your job application

🔐 Built-in Authentication
Bearer token authentication (required by Puch AI)

Validation tool that returns your phone number

Quick Setup Guide
Step 1: Install Dependencies
Make sure you have Python 3.11 or higher installed. Then:

bash
Copy
Edit
# Create virtual environment
uv venv

# Install all required packages
uv sync

# Activate the environment
source .venv/bin/activate
Step 2: Set Up Environment Variables
Create a .env file in the project root:

bash
Copy
Edit
# Copy the example file
cp .env.example .env
Then edit .env and add your details:

env
Copy
Edit
AUTH_TOKEN=your_secret_token_here
MY_NUMBER=919876543210
OPENAI_API_KEY=your_openai_api_key_here
Important Notes:

AUTH_TOKEN: This is your secret token for authentication. Keep it safe!

MY_NUMBER: Your WhatsApp number in format {country_code}{number} (e.g., 919876543210 for +91-9876543210)

OPENAI_API_KEY: Your OpenAI API key for using the interview coach tool

Step 3: Run the Server
bash
Copy
Edit
cd mcp-bearer-token
python mcp_starter.py
You'll see: 🚀 Starting MCP server on http://0.0.0.0:8086

Step 4: Make It Public (Required by Puch)
Since Puch needs to access your server over HTTPS, you need to expose your local server:

Option A: Using ngrok (Recommended)
Install ngrok:
Download from https://ngrok.com/download

Get your authtoken:

Go to https://dashboard.ngrok.com/get-started/your-authtoken

Copy your authtoken

Run: ngrok config add-authtoken YOUR_AUTHTOKEN

Start the tunnel:

bash
Copy
Edit
ngrok http 8086
Option B: Deploy to Cloud
You can also deploy this to services like:

Railway

Render

Heroku

DigitalOcean App Platform

How to Connect with Puch AI
Open Puch AI in your browser

Start a new conversation

Use the connect command:

arduino
Copy
Edit
/mcp connect https://your-domain.ngrok.app/mcp your_secret_token_here
Debug Mode
To get more detailed error messages:

pgsql
Copy
Edit
/mcp diagnostics-level debug
Custom Tools in This Starter
Interview Coach Tool
This tool uses OpenAI to analyze your resume, job description, and interview answers and then provide feedback.

Inputs
resume_text: Your full resume as text

job_description: The job description text you are applying for

interview_answer: Your answer to an interview question

Output
Suggestions to improve your resume to better match the job

Feedback on your interview answer

Tips to improve your interview performance

Example Usage
python
Copy
Edit
response = interview_coach(
    resume_text="Experienced Java developer with 5 years of backend development...",
    job_description="We are looking for a full-stack Java developer with React experience...",
    interview_answer="My biggest strength is my ability to learn quickly and solve complex problems..."
)
print(response.text)
How to Add Your Own Tools
Create a new tool function:

python
Copy
Edit
@mcp.tool(description="Your tool description")
async def your_tool_name(
    parameter: Annotated[str, Field(description="Parameter description")]
) -> str:
    # Your tool logic here
    return "Tool result"
Add required imports if needed.

📚 Additional Documentation Resources
Official Puch AI MCP Documentation: https://puch.ai/mcp

Core MCP protocol and commands

JSON-RPC 2.0 Specification: https://www.jsonrpc.org/specification

Getting Help
Join Puch AI Discord: https://discord.gg/VMCnMvYx

Check Puch AI MCP docs: https://puch.ai/mcp

Puch WhatsApp Number: +91 99988 81729

Happy coding! 🚀

Use the hashtag #BuildWithPuch in your posts about your MCP!
