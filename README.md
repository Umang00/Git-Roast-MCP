---
title: GitRoast MCP Server
emoji: 🔥
colorFrom: red
colorTo: yellow
sdk: gradio
sdk_version: "6.0.0"
app_file: app.py
pinned: false
tags:
  - mcp
  - building-mcp-track-consumer
  - gradio
  - github
  - ai
  - roast
  - model-context-protocol
  - gemini
license: mit
---

# 🔥 GitRoast MCP Server

**Brutally roast GitHub repositories using AI-powered analysis and savage humor.**

Built for the **[MCP 1st Birthday Hackathon](https://huggingface.co/MCP-1st-Birthday)** (Track 1: Building MCP - Consumer) using **Gradio 6**.

[![Gradio](https://img.shields.io/badge/Gradio-6.0-orange)](https://gradio.app/)
[![MCP](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io/)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org/)

---

## 📺 Demo Video

> **[🎥 Watch 3-Minute Demo](YOUR_YOUTUBE_LINK_HERE)**
>
> See GitRoast in action: analyzing repos, generating AI roasts, and integrating with Claude Desktop via MCP!

---

## 📱 Social Media

> **[🐦 Twitter/X Post](YOUR_TWITTER_LINK_HERE)** | **[💼 LinkedIn Post](YOUR_LINKEDIN_LINK_HERE)**
>
> Share your roast results with **#GitRoast #MCPFirstBirthday**!

---

## ✨ What is GitRoast?

GitRoast is a **Model Context Protocol (MCP) server** that analyzes GitHub repositories and profiles, then generates **hilariously brutal but constructive roasts** based on:

- 💀 **Commit Patterns** - Late-night coding, weekend commits, frequency analysis
- 📝 **Message Quality** - Lazy commits ("fix", "wip", "asdf"), clarity, length
- 📄 **Documentation** - README quality, code examples, installation instructions
- 🏷️ **Repository Health** - Description, license, topics, archived status
- 🏆 **Achievements** - Embarrassing badges based on patterns
- 💡 **Suggestions** - Brutally honest but helpful feedback

**Plus:** It works as an **MCP server**, making it accessible to Claude Desktop, Claude Code, Cursor, and any MCP-compatible AI agent!

---

## 🎮 Try It Now!

### Web Interface

1. Enter a GitHub repository URL or username above
2. Click **"🔥 Roast This Repo!"**
3. Enjoy the brutal roast!

**Examples to try:**
- `facebook/react`
- `torvalds/linux`
- `octocat` (GitHub profile)

### As an MCP Server

Connect this Space as an MCP server to Claude Desktop or Cursor:

**Claude Desktop** - Edit `%APPDATA%\Claude\claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "https://YOUR_USERNAME-gitroast-mcp.hf.space/gradio_api/mcp/"
      ]
    }
  }
}
```

**Cursor** - Edit `~/.cursor/mcp.json`:
```json
{
  "mcpServers": {
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "https://YOUR_USERNAME-gitroast-mcp.hf.space/gradio_api/mcp/"
      ]
    }
  }
}
```

Replace `YOUR_USERNAME` with your Hugging Face username.

**Then ask Claude or Cursor:**
```
Use GitRoast to analyze the repository facebook/react
```

---

## 🏆 MCP 1st Birthday Hackathon

**Track:** Track 1 - Building MCP (Consumer)
**Tag:** `building-mcp-track-consumer`

### Why GitRoast?

✅ **Novel MCP Use Case** - First MCP server for code roasting
✅ **Google Gemini Integration** - Sponsor technology for AI roasts
✅ **Educational + Entertaining** - Learn from brutal feedback
✅ **Production-Ready** - Built with Gradio 6 native MCP support
✅ **Universal Compatibility** - Works with any MCP client

### What Makes It Special

- **Unique Concept** - Roasting code with AI via MCP (nobody else is doing this!)
- **Dual Analysis Modes** - Analyze single repos OR entire user profiles
- **Comprehensive Analysis** - 10+ metrics tracked per repository
- **Smart Fallback** - AI roasts with template fallback (always works)
- **Achievement System** - Gamified feedback with embarrassing badges
- **Clean Architecture** - Well-documented, type-safe, maintainable code

### Judging Criteria Alignment

| Criteria | How GitRoast Delivers |
|----------|----------------------|
| **Completeness** | ✅ HF Space + Social Post + Documentation + Demo Video |
| **Design/UI-UX** | ✅ Clean Gradio 6 interface, intuitive workflow |
| **Functionality** | ✅ Native Gradio 6 MCP, AI integration, dual modes |
| **Creativity** | ✅ Novel concept: roasting code with AI humor |
| **Documentation** | ✅ Comprehensive README + demo video |
| **Real-world Impact** | ✅ Educational feedback for developers |

---

## 📊 Features

### Comprehensive Analysis

**Commit Pattern Detection:**
- Late-night commits (11 PM - 5 AM)
- Weekend coding frequency
- Commit message quality scoring
- Fix/WIP/Merge commit ratios
- Author count and contribution patterns

**Documentation Quality:**
- README completeness and length
- Code examples presence
- Installation instructions
- License detection
- Repository topics/tags

**Repository Health:**
- Meaningful description check
- License verification
- Topic/tag completeness
- Archived/abandoned detection
- Star/fork/issue metrics

### AI-Powered Roasts

**Google Gemini Integration:**
- Creative, personalized roasts based on actual patterns
- Context-aware humor tailored to your code
- Savage but constructive feedback
- Multiple roast categories (6-10 per analysis)

**Template Fallback:**
- Pre-written savage roasts for common patterns
- Works without API key
- Still funny and useful
- Instant results

**Achievement System:**
- "Vampire Code Goblin" (too many late-night commits)
- "Weekend Prisoner" (no life outside code)
- "Commit Message War Criminal" (lazy messages)
- "Industrial Bug Factory" (too many fix commits)
- And 10+ more embarrassing badges!

**Constructive Suggestions:**
- Brutally honest but actionable advice
- Specific improvements for your workflow
- Best practices recommendations
- Documentation tips

### Dual Analysis Modes

**Repository Analysis:**
- Deep dive into a single repository
- All commits analyzed (up to 1,000)
- README and metadata review
- Detailed pattern detection

**Profile Analysis:**
- Analyze user's entire coding history
- Aggregates data from all public repos
- Cross-repository pattern detection
- Identifies coding habits across projects

---

## 🛠️ Tech Stack

**MCP Integration:**
- [Gradio 6](https://gradio.app/) - Native MCP server support (`mcp_server=True`)
- [Model Context Protocol](https://modelcontextprotocol.io/) - Standard protocol compliance
- Server-Sent Events (SSE) - Real-time communication
- JSON-RPC - Request/response handling

**AI & APIs:**
- [Google Gemini](https://ai.google.dev/) - AI roast generation (gemini-2.5-flash)
- [GitHub API](https://docs.github.com/en/rest) - Repository and commit data
- Retry logic with exponential backoff
- Rate limit handling (60/hr → 5000/hr with token)

**Core Technologies:**
- Python 3.8+ - Type-safe implementation
- Gradio 6.0 - Web UI and MCP server
- `requests` - HTTP client
- `python-dotenv` - Environment management

---

## 🔑 API Keys (Optional)

This Space works **without API keys**, but you can add them for better results:

### GitHub Token

**Benefits:**
- Increases rate limit from 60 to 5,000 requests/hour
- Allows analyzing more repositories
- Faster analysis for profiles

**How to get:**
1. Go to [GitHub Settings → Tokens](https://github.com/settings/tokens)
2. Generate new token (classic)
3. **No scopes needed** (we only read public repos)
4. Copy token

**How to use:**
- Enter in "Optional API Keys" accordion above, OR
- Add as Space Secret: `GITHUB_TOKEN`

### Gemini API Key

**Benefits:**
- AI-generated creative roasts
- Personalized humor based on your patterns
- Better than templates (but templates are still good!)

**How to get:**
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with Google account
3. Create API Key
4. Copy key

**How to use:**
- Enter in "Optional API Keys" accordion above, OR
- Add as Space Secret: `GEMINI_API_KEY`

---

## 🚀 Usage Examples

### Example 1: Analyze a Popular Repository

**Input:** `facebook/react`

**Output:**
```
🔥 GitRoast Results - Grade: B

Pretty good! Not perfect, but you're not actively making the world worse.

📦 Repository: facebook/react
- Stars: 220,000+
- Language: JavaScript

📊 Quick Stats
- Total Commits: 15,234
- Late Night Commits: 4,870 (32%)

🔥 The Roasts (6)

1. 🦉 Certified Nocturnal Disaster 🔥🔥🔥🔥🔥
32% of your commits are between 11 PM and 5 AM...
[Full roast content]

🏆 Achievements (3)
- 🌙 Vampire Code Goblin
  4,870 commits made while humanity sleeps...

💡 Suggestions
- Get some sleep. Your code quality drops 50% after midnight...
```

### Example 2: Analyze a GitHub Profile

**Input:** `octocat`

**Output:**
Analyzes all public repositories, combines statistics, identifies cross-repo patterns, and generates a comprehensive profile roast.

### Example 3: MCP Integration with Claude

**User:** "Use GitRoast to analyze my repository github.com/myuser/myproject"

**Claude:** *Calls GitRoast MCP server*

**GitRoast:** Returns complete analysis with roasts, achievements, and suggestions

**Claude:** Presents results in a conversational format, can discuss patterns, answer questions about the analysis

---

## 📖 Setup & Installation

### For Local Development

1. **Clone repository:**
   ```bash
   git clone https://github.com/Umang00/Git-Roast-MCP.git
   cd Git-Roast-MCP
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment (optional):**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

4. **Run the server:**
   ```bash
   python app.py
   ```

5. **Access:**
   - Web UI: http://localhost:7860
   - MCP Endpoint: http://localhost:7860/gradio_api/mcp/

### For MCP Client Integration

**Claude Desktop:**
```json
{
  "mcpServers": {
    "gitroast": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sse-client",
        "http://localhost:7860/gradio_api/mcp/"
      ]
    }
  }
}
```

Restart Claude Desktop and ask:
```
Use GitRoast to analyze facebook/react
```

**Cursor IDE:**
Edit `~/.cursor/mcp.json` with same configuration as above.

**Any MCP Client:**
Connect to: `http://localhost:7860/gradio_api/mcp/` using SSE transport

---

## 🏗️ Architecture

```
┌─────────────────────┐
│  MCP Clients        │
│  (Claude Desktop,   │
│   Cursor, etc.)     │
└──────────┬──────────┘
           │ stdio
           ↓
┌─────────────────────┐
│  NPX Bridge         │
│  server-sse-client  │
└──────────┬──────────┘
           │ HTTP/SSE
           ↓
┌─────────────────────┐
│  Gradio MCP Server  │
│  (app.py)           │
│  - Native Gradio 6  │
│  - mcp_server=True  │
└──────────┬──────────┘
           │
           ↓
┌─────────────────────┐
│  analyze_repo()     │
│  (logic.py)         │
│  - Type-safe        │
│  - Docstrings       │
│  - Error handling   │
└──────────┬──────────┘
           │
      ┌────┴────┐
      ↓         ↓
┌──────────┐ ┌──────────┐
│ GitHub   │ │ Gemini   │
│   API    │ │   API    │
└──────────┘ └──────────┘
```

**Key Design Decisions:**

1. **Native Gradio 6 MCP** - No custom bridge needed
2. **Clean Separation** - UI (app.py) + Logic (logic.py)
3. **Type Safety** - Full type hints for MCP compatibility
4. **Smart Fallback** - Template roasts if AI fails
5. **Retry Logic** - Exponential backoff for API calls

---

## 📁 Project Structure

```
git-roast-mcp/
├── app.py                 # Gradio UI + MCP server
├── logic.py               # Analysis & roast generation (1,363 lines)
├── requirements.txt       # Dependencies
├── pyproject.toml         # Project metadata
├── .env.example           # Environment template
├── README.md              # This file
└── docs/                  # Additional documentation
    ├── SETUP.md           # Detailed setup guide
    ├── DEPLOYMENT.md      # Deployment instructions
    └── HACKATHON.md       # Hackathon submission notes
```

---

## 🐛 Troubleshooting

### Common Issues

**"Rate limit exceeded"**
- Add GitHub token (increases limit from 60 to 5,000 req/hr)
- Add as Space Secret or enter in UI

**"MCP server not connecting"**
- Make sure Space/server is running
- Check MCP endpoint URL is correct
- Restart MCP client (Claude Desktop/Cursor)
- Verify `npx` is installed (comes with Node.js)

**"AI roast generation failed"**
- Check Gemini API key is valid
- Don't worry - automatically falls back to template roasts
- Templates are still funny and useful!

**"Repository not found"**
- Make sure repository is public
- Check URL format (owner/repo)
- Try accessing repo in browser first

### Browser Errors (Normal!)

If you see errors like:
```
ERROR:mcp.server.streamable_http:Error handling POST request
ClientDisconnect
```

**This is NORMAL!** MCP endpoints are designed for MCP clients (Claude Desktop, Cursor), not browsers. The web UI at the root URL works fine - these errors only appear when browsers try to access the MCP endpoint directly.

---

## 🤝 Contributing

This is a hackathon project, but contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

**Ideas for contributions:**
- Additional roast templates
- More achievement badges
- Support for other code hosting platforms
- Language-specific analysis
- Code complexity metrics

---

## 📄 License

MIT License - See repository for details

---

## 👥 Team

**Solo Developer:** [@Umang00](https://github.com/Umang00)

Built with ❤️ for the MCP community and developers who can take a joke!

---

## 🙏 Acknowledgments

- **MCP 1st Birthday Hackathon** - For the opportunity and inspiration
- **[Gradio](https://gradio.app/)** - Amazing framework with native MCP support
- **[Google Gemini](https://ai.google.dev/)** - Powering the AI roasts
- **[Anthropic](https://anthropic.com/)** - For creating the MCP protocol
- **GitHub Community** - For the public APIs and data

---

## ⚠️ Disclaimer

This tool is for **entertainment and educational purposes only**.

The roasts are meant to be:
- ✅ Funny and lighthearted
- ✅ Constructive (pointing out real patterns)
- ✅ Educational (highlighting best practices)
- ❌ NOT mean-spirited or personal attacks

**Use responsibly and don't take it too seriously!** 😄

Remember: The best developers can laugh at their commit history while learning from it.

---

## 🔗 Links

- **🏠 Live Demo:** [YOUR_HF_SPACE_URL]
- **📺 Demo Video:** [YOUR_YOUTUBE_LINK]
- **💻 GitHub:** https://github.com/Umang00/Git-Roast-MCP
- **🐦 Twitter:** [YOUR_TWITTER_POST]
- **💼 LinkedIn:** [YOUR_LINKEDIN_POST]
- **📖 MCP Documentation:** https://modelcontextprotocol.io/
- **🎨 Gradio MCP Guide:** https://www.gradio.app/guides/building-mcp-server-with-gradio

---

**Made with 🔥 and ☕ for the MCP 1st Birthday Hackathon**

**Track 1: Building MCP | Tag: `building-mcp-track-consumer`**
