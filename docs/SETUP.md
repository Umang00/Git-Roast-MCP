# GitRoast MCP Server - Complete Setup Guide

This guide covers all setup methods for using GitRoast as an MCP server.

## Table of Contents

- [Quick Start](#quick-start)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Claude Desktop Setup](#claude-desktop-setup)
- [Claude Code Setup](#claude-code-setup)
- [Environment Variables](#environment-variables)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)

---

## Quick Start

**3 steps to get running:**

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Start the server:**
   ```bash
   python app.py
   ```

3. **Configure your MCP client** (see sections below)

---

## Prerequisites

### Required
- **Python 3.8+** (3.13+ recommended)
- **Node.js 18+** (for Claude Desktop MCP bridge)
- **Git** (for cloning the repository)

### Optional but Recommended
- **GitHub Personal Access Token** - For higher rate limits (5000 vs 60 req/hr)
- **Google Gemini API Key** - For AI-powered roasts (falls back to templates without it)

### Check Prerequisites

```bash
# Check Python
python --version

# Check Node.js (required for Claude Desktop)
node --version
npx --version

# Check Git
git --version
```

**Don't have Node.js?** Download from: https://nodejs.org/

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/git-roast-mcp.git
cd git-roast-mcp
```

### 2. Install Python Dependencies

```bash
pip install -r requirements.txt
```

**Dependencies installed:**
- `gradio[mcp]>=6.0.0` - Web UI and MCP server
- `requests>=2.31.0` - GitHub API calls
- `google-generativeai>=0.3.0` - AI roast generation
- `python-dotenv>=1.0.0` - Environment variables
- `sseclient>=0.0.27` - SSE client (for bridge)

### 3. Configure Environment (Optional)

Create a `.env` file in the project root:

```bash
GITHUB_TOKEN=ghp_your_github_token_here
GEMINI_API_KEY=your_gemini_api_key_here
GEMINI_MODEL=gemini-2.5-flash-preview-09-2025
```

See [Environment Variables](#environment-variables) section for details.

### 4. Start the Server

```bash
python app.py
```

You should see:
```
* Running on local URL: http://127.0.0.1:7860
* Streamable HTTP URL: http://127.0.0.1:7860/gradio_api/mcp/
```

**Keep this terminal open!** The server must stay running for MCP to work.

---

## Claude Desktop Setup

### How It Works

With Gradio 6, the MCP setup is simple:

```
Claude Desktop
    ↓ (stdio)
npx @modelcontextprotocol/server-sse-client (auto-installed bridge)
    ↓ (HTTP/SSE)
Your Gradio Server (app.py)
    ↓
analyze_repo() function
```

### Configuration Steps

#### 1. Find Your Config File

**Windows:**
```
C:\Users\<YourUsername>\AppData\Roaming\Claude\claude_desktop_config.json
```

**Quick access on Windows:**
- Press `Win + R`
- Type: `%APPDATA%\Claude\claude_desktop_config.json`
- Press Enter

**macOS:**
```
~/Library/Application Support/Claude/claude_desktop_config.json
```

**Linux:**
```
~/.config/Claude/claude_desktop_config.json
```

#### 2. Edit the Config File

If the file doesn't exist, create it. Add this configuration:

```json
{
  "mcpServers": {
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "http://127.0.0.1:7860/gradio_api/mcp/"
      ]
    }
  }
}
```

**If you already have other MCP servers**, just add the `gitroast` entry:

```json
{
  "mcpServers": {
    "existing-server": {
      ...
    },
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "http://127.0.0.1:7860/gradio_api/mcp/"
      ]
    }
  }
}
```

#### 3. Restart Claude Desktop

1. **Close Claude Desktop completely** (check system tray/taskbar)
2. **Reopen Claude Desktop**
3. Wait a few seconds for the MCP server to connect

#### 4. Verify Connection

- Look for the 🔌 icon or tools indicator in Claude Desktop
- GitRoast should appear in the list of available tools

#### 5. Test It

Try these prompts:

```
Use GitRoast to analyze the repository facebook/react
```

```
Roast the GitHub profile: torvalds
```

```
What are the commit patterns for microsoft/vscode using GitRoast?
```

---

## Claude Code Setup

### How It Works

Claude Code (CLI) uses the same NPX bridge as Claude Desktop.

### Configuration Steps

#### 1. Find Your Config File

**Windows:**
```
C:\Users\<YourUsername>\.claude\config.json
```

**macOS/Linux:**
```
~/.claude/config.json
```

#### 2. Create/Edit the Config

```json
{
  "mcpServers": {
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "http://127.0.0.1:7860/gradio_api/mcp/"
      ]
    }
  }
}
```

#### 3. Restart Claude Code

Close and reopen your Claude Code session.

#### 4. Test It

Ask Claude Code to use GitRoast:

```
Use GitRoast to analyze facebook/react
```

---

## Environment Variables

### Option 1: .env File (Recommended)

Create `.env` in the project root:

```bash
# GitHub API (optional but recommended)
GITHUB_TOKEN=ghp_your_token_here

# Gemini API (optional - for AI roasts)
GEMINI_API_KEY=your_gemini_key_here
GEMINI_MODEL=gemini-2.5-flash-preview-09-2025
```

### Option 2: System Environment Variables

**Windows:**
```powershell
setx GITHUB_TOKEN "ghp_your_token_here"
setx GEMINI_API_KEY "your_gemini_key_here"
```

**macOS/Linux:**
```bash
export GITHUB_TOKEN="ghp_your_token_here"
export GEMINI_API_KEY="your_gemini_key_here"
```

### Getting API Keys

#### GitHub Personal Access Token

1. Go to: https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Name it "GitRoast"
4. **No scopes needed** (we only read public repos)
5. Copy the token

**Why use a token?**
- Without: 60 requests/hour
- With: 5,000 requests/hour

#### Google Gemini API Key

1. Go to: https://makersuite.google.com/app/apikey
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy the key

**Why use Gemini?**
- Without: Template-based roasts (still funny)
- With: AI-generated personalized roasts

---

## Testing

### Test the Web UI

1. Start the server: `python app.py`
2. Open browser: http://127.0.0.1:7860
3. Enter a GitHub repo URL (e.g., `facebook/react`)
4. Click "🔥 Roast This Repo!"

If this works, your server is running correctly.

### Test the MCP Endpoint

The MCP endpoint is at: http://127.0.0.1:7860/gradio_api/mcp/

**Note:** Don't test this in a browser - it's designed for MCP clients, not browsers. You'll see errors if you access it directly.

### Test with Claude Desktop/Code

Ask Claude to use GitRoast:

```
Use GitRoast to analyze the repository tensorflow/tensorflow
```

Claude should automatically call the MCP tool and return roast results.

---

## Troubleshooting

### "MCP server failed to connect"

**Check 1: Is the Gradio server running?**
```bash
python app.py
```
Keep this terminal open!

**Check 2: Is Node.js installed?**
```bash
node --version
npx --version
```
If not, install from: https://nodejs.org/

**Check 3: Is the port available?**
```bash
# Windows
netstat -an | findstr 7860

# macOS/Linux
lsof -i :7860
```

**Check 4: Try accessing the web UI**
Open: http://127.0.0.1:7860

If this doesn't work, the server isn't running properly.

### "Module not found"

Reinstall dependencies:
```bash
pip install -r requirements.txt
```

Make sure all these are installed:
- gradio[mcp]
- requests
- google-generativeai
- python-dotenv
- sseclient

### "Rate limit exceeded"

Add a GitHub token to your `.env` file:
```bash
GITHUB_TOKEN=ghp_your_token_here
```

This increases rate limit from 60 to 5,000 requests/hour.

### Config File Syntax Errors

Make sure your JSON is valid:
- Use double quotes `"`, not single quotes `'`
- Don't forget commas between entries
- Check for matching brackets `{}`

**Validate JSON:** https://jsonlint.com/

### Server Won't Start

**Error: "Port 7860 already in use"**

Kill the existing process:
```bash
# Windows
netstat -ano | findstr :7860
taskkill /PID <process_id> /F

# macOS/Linux
lsof -ti:7860 | xargs kill -9
```

Or change the port in `app.py`:
```python
demo.launch(
    mcp_server=True,
    server_port=7861  # Use a different port
)
```

### Firewall Issues

Make sure Python is allowed through your firewall:

**Windows:**
- Windows Security → Firewall & network protection
- Allow an app through firewall
- Find Python → Allow private and public networks

**macOS:**
- System Preferences → Security & Privacy → Firewall
- Firewall Options → Add Python

### Still Having Issues?

1. **Check the terminal** where `python app.py` is running for error messages
2. **Check Claude Desktop logs** (Windows: `%APPDATA%\Claude\logs\`)
3. **Try the web UI first** to isolate if it's an MCP issue or server issue
4. **Restart everything**: Server, Claude Desktop/Code, terminal

---

## Verification Checklist

Before asking for help, verify:

- [ ] Python 3.8+ is installed
- [ ] Node.js 18+ is installed (for Claude Desktop)
- [ ] Dependencies installed: `pip install -r requirements.txt`
- [ ] Server is running: `python app.py`
- [ ] Web UI works: http://127.0.0.1:7860
- [ ] Config file exists and has correct JSON syntax
- [ ] Claude Desktop/Code has been restarted
- [ ] No firewall blocking localhost connections

---

## Advanced Usage

### Using a Different Port

Edit `app.py`:
```python
demo.launch(
    mcp_server=True,
    server_port=8080  # Change port
)
```

Update your MCP config:
```json
"args": [
  "-y",
  "@modelcontextprotocol/server-sse-client",
  "http://127.0.0.1:8080/gradio_api/mcp/"
]
```

### Running on a Remote Server

To access from another machine:

```python
demo.launch(
    mcp_server=True,
    server_name="0.0.0.0",  # Listen on all interfaces
    server_port=7860
)
```

Update MCP config with server IP:
```json
"args": [
  "-y",
  "@modelcontextprotocol/server-sse-client",
  "http://192.168.1.100:7860/gradio_api/mcp/"
]
```

### Using with SSL/HTTPS

For production, use a reverse proxy (nginx, Caddy) with SSL.

---

## Next Steps

- **For hackathon submission:** See [docs/HACKATHON.md](HACKATHON.md)
- **For deployment:** See [docs/DEPLOYMENT.md](DEPLOYMENT.md)
- **For development:** See main [README.md](../README.md)

---

## Resources

- **Gradio MCP Docs:** https://www.gradio.app/guides/mcp
- **MCP Protocol:** https://modelcontextprotocol.io/
- **GitHub API:** https://docs.github.com/en/rest
- **Gemini API:** https://ai.google.dev/docs
