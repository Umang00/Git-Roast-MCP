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

Built for the **MCP 1st Birthday Hackathon (Track 1: Building MCP)** using Gradio 6..

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

## 🎮 Try It Now!

### Web Interface

Just enter a GitHub repository URL or username above and click "🔥 Roast This Repo!"

**Examples to try:**
- `facebook/react`
- `torvalds/linux`
- `octocat` (GitHub profile)

### As an MCP Server

Connect this Space as an MCP server to Claude Desktop:

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

**Then ask Claude:**
```
Use GitRoast to analyze the repository facebook/react
```

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

---

## 🔑 API Keys (Optional)

This Space works without API keys, but you can add them for better results:

### GitHub Token

**Why:** Increases rate limit from 60 to 5,000 requests/hour

**How to add:**
1. Get token from [GitHub Settings](https://github.com/settings/tokens) (no scopes needed)
2. Enter in the "Optional API Keys" accordion above

### Gemini API Key

**Why:** Enables AI-powered roasts (falls back to templates without it)

**How to add:**
1. Get key from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Enter in the "Optional API Keys" accordion above

**Note:** For permanent deployment, add these as Space Secrets in Settings.

---

## 🛠️ Tech Stack

- **[Gradio 6](https://gradio.app/)** - Web UI and native MCP server support
- **[Google Gemini](https://ai.google.dev/)** - AI-powered roast generation
- **[GitHub API](https://docs.github.com/en/rest)** - Repository and commit data
- **[Model Context Protocol](https://modelcontextprotocol.io/)** - AI agent integration
- **Python 3.8+** - Core language

---

## 📖 Documentation

Full documentation available at the [GitHub repository](https://github.com/your-username/git-roast-mcp):

- **Setup Guide** - Complete installation and configuration
- **Hackathon Submission** - MCP 1st Birthday submission guide
- **Deployment Guide** - Deploy to various platforms

---

## ⚠️ Disclaimer

This tool is for **entertainment and educational purposes only**. The roasts are meant to be funny and constructive, not mean-spirited. Use responsibly and don't take it too seriously! 😄

---

## 📄 License

MIT License - See repository for details

---

**Made with 🔥 and ☕ for the MCP 1st Birthday Hackathon**

GitHub: [your-username/git-roast-mcp](https://github.com/your-username/git-roast-mcp)
