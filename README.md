# 🔥 GitRoast MCP Server

**Brutally roast GitHub repositories using AI-powered analysis and savage humor.**

Built for the **MCP 1st Birthday Hackathon (Track 1: Building MCP)** using Gradio 6.

[![Gradio](https://img.shields.io/badge/Gradio-6.0-orange)](https://gradio.app/)
[![MCP](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io/)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org/)

---

## ✨ What is GitRoast?

GitRoast analyzes GitHub repositories and profiles, then generates **hilariously brutal roasts** based on:

- 💀 Commit patterns (late-night coding, weekend commits)
- 📝 Commit message quality (or lack thereof)
- 📄 Documentation completeness
- 🏷️ Repository metadata
- 🏆 Embarrassing achievements
- 💡 Brutally honest suggestions

**Plus:** It works as an **MCP server**, making it accessible to Claude Desktop, Claude Code, and any MCP-compatible AI agent!

---

## 🎥 Demo

> **[📺 Watch Demo Video](#)** _(Coming soon for hackathon submission)_

![GitRoast Demo](https://via.placeholder.com/800x400?text=GitRoast+Demo+Screenshot)

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Start the Server

```bash
python app.py
```

### 3. Use It!

**Web Interface:**
Open http://127.0.0.1:7860 in your browser

**With Claude Desktop:**
See [Setup Guide](docs/SETUP.md#claude-desktop-setup) for MCP configuration

---

## 🔌 MCP Integration

### Claude Desktop Configuration

Add this to your `claude_desktop_config.json`:

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

**Then ask Claude:**
```
Use GitRoast to analyze the repository facebook/react
```

**Full setup instructions:** See [docs/SETUP.md](docs/SETUP.md)

---

## 📊 Features

### Comprehensive Analysis

- **Commit Patterns**: Late-night commits, weekend coding, frequency analysis
- **Message Quality**: Length, clarity, lazy commits ("fix", "wip", "asdf")
- **Documentation**: README quality, code examples, installation instructions
- **Repository Health**: Description, license, topics, archived status

### AI-Powered Roasts

- **Google Gemini Integration**: Generates creative, personalized roasts
- **Template Fallback**: Works without API key using savage pre-written roasts
- **Achievement System**: Unlocks embarrassing badges based on patterns
- **Constructive Feedback**: Brutal but actually helpful suggestions

### Dual Analysis Modes

- **Repository Analysis**: Analyze a single repo in depth
- **Profile Analysis**: Analyze a user's entire coding history across repos

### MCP Server

- **Native Gradio 6 Support**: Built-in MCP server functionality
- **Standards-Compliant**: Works with any MCP client
- **Type-Safe**: Proper type hints and docstrings
- **Auto-Discovery**: Tools are automatically exposed to AI agents

---

## 🎯 Usage Examples

### Analyze a Repository

**Input:**
```
facebook/react
```

**Output:**
```markdown
# 🔥 GitRoast Results - Grade: B

**Pretty good! Not perfect, but you're not actively making the world worse.**

### 📦 Repository: facebook/react
- Stars: 220,000
- Language: JavaScript

### 🔥 The Roasts (6)

1. 🦉 Certified Nocturnal Disaster 🔥🔥🔥🔥🔥
32% of commits between 11 PM and 5 AM. Are you okay? Seriously...

[Full roast results with stats, achievements, suggestions]
```

### Analyze a GitHub Profile

**Input:**
```
octocat
```

**Output:**
Analyzes all public repositories and generates combined statistics and roasts.

---

## 📚 Documentation

- **[Setup Guide](docs/SETUP.md)** - Complete installation and configuration
- **[Hackathon Submission](docs/HACKATHON.md)** - MCP 1st Birthday submission guide
- **[Deployment Guide](docs/DEPLOYMENT.md)** - Deploy to Hugging Face, Docker, cloud

---

## 🔑 API Keys (Optional)

### GitHub Token

**Why:** Increases rate limit from 60 to 5,000 requests/hour

**Get it:** [GitHub Settings → Tokens](https://github.com/settings/tokens)

**Add to `.env`:**
```bash
GITHUB_TOKEN=ghp_your_token_here
```

### Gemini API Key

**Why:** Enables AI-powered roasts (falls back to templates without it)

**Get it:** [Google AI Studio](https://makersuite.google.com/app/apikey)

**Add to `.env`:**
```bash
GEMINI_API_KEY=your_key_here
GEMINI_MODEL=gemini-2.5-flash-preview-09-2025
```

---

## 🏗️ Architecture

```
┌─────────────────┐
│  Claude Desktop │
│   Claude Code   │
└────────┬────────┘
         │ stdio
         ↓
┌─────────────────┐
│      npx        │
│  server-sse-    │
│     client      │
└────────┬────────┘
         │ HTTP/SSE
         ↓
┌─────────────────┐
│  Gradio MCP     │
│    Server       │
│   (app.py)      │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│  analyze_repo() │
│   (logic.py)    │
└────────┬────────┘
         │
    ┌────┴────┐
    ↓         ↓
┌────────┐ ┌─────────┐
│ GitHub │ │ Gemini  │
│  API   │ │   API   │
└────────┘ └─────────┘
```

---

## 🛠️ Tech Stack

- **[Gradio 6](https://gradio.app/)** - Web UI and native MCP server support
- **[Google Gemini](https://ai.google.dev/)** - AI-powered roast generation
- **[GitHub API](https://docs.github.com/en/rest)** - Repository and commit data
- **[Model Context Protocol](https://modelcontextprotocol.io/)** - AI agent integration
- **Python 3.8+** - Core language

---

## 🏆 MCP 1st Birthday Hackathon

**Track:** Track 1 - Building MCP (Consumer)

**Why GitRoast?**
- ✅ Novel use of MCP for developer tools
- ✅ Integrates Google Gemini AI (sponsor technology)
- ✅ Educational + entertaining
- ✅ Production-ready with Gradio 6
- ✅ Works with any MCP client

**What makes it special:**
- Unique concept: roasting code with AI via MCP
- Dual analysis modes (repos + profiles)
- Comprehensive commit pattern analysis
- Embarrassing but constructive achievements
- Clean architecture and good documentation

**Submission Details:** See [docs/HACKATHON.md](docs/HACKATHON.md)

---

## 📁 Project Structure

```
git-roast-mcp/
├── app.py                 # Gradio interface + MCP server
├── logic.py               # Core analysis and roast logic
├── requirements.txt       # Python dependencies
├── pyproject.toml         # Project metadata
├── .env.example           # Environment variable template
├── README.md              # This file
└── docs/
    ├── SETUP.md           # Complete setup guide
    ├── HACKATHON.md       # Hackathon submission guide
    └── DEPLOYMENT.md      # Deployment instructions
```

---

## 🐛 Troubleshooting

### Common Issues

**Server won't start:**
```bash
pip install -r requirements.txt
python app.py
```

**MCP not connecting:**
- Make sure `python app.py` is running
- Check Claude Desktop config has correct URL
- Restart Claude Desktop after config changes

**Rate limit errors:**
- Add `GITHUB_TOKEN` to `.env`
- Increases limit to 5,000 requests/hour

**Full troubleshooting guide:** See [docs/SETUP.md#troubleshooting](docs/SETUP.md#troubleshooting)

---

## 🤝 Contributing

This is a hackathon project, but contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📄 License

MIT License - See LICENSE file for details

---

## 🙏 Acknowledgments

- Built for the **MCP 1st Birthday Hackathon**
- Powered by [Gradio](https://gradio.app/) and [Google Gemini](https://ai.google.dev/)
- Inspired by the original GitRoast project
- Thanks to the MCP community

---

## ⚠️ Disclaimer

This tool is for **entertainment and educational purposes only**. The roasts are meant to be funny and constructive, not mean-spirited. Use responsibly and don't take it too seriously! 😄

---

## 📞 Contact

- **Issues:** [GitHub Issues](https://github.com/your-username/git-roast-mcp/issues)
- **Discussions:** [GitHub Discussions](https://github.com/your-username/git-roast-mcp/discussions)
- **Social:** [Twitter](#) | [LinkedIn](#)

---

**Made with 🔥 and ☕ for the MCP 1st Birthday Hackathon**
