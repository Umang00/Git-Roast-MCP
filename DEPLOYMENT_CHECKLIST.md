# Hugging Face Spaces Deployment Checklist

## ✅ Pre-Deployment Verification

Based on [Gradio 6 MCP deployment requirements](https://www.gradio.app/guides/building-mcp-server-with-gradio) and [Hugging Face Spaces documentation](https://huggingface.co/docs/hub/en/spaces-sdks-gradio).

### Files Ready ✓

- [x] `app.py` - Updated with environment variable support
- [x] `logic.py` - Core analysis logic
- [x] `requirements.txt` - Cleaned up (removed sseclient)
- [x] `README_HF_SPACES.md` - Ready to rename to README.md for Spaces

### Code Changes Made ✓

**app.py changes:**
- [x] Changed `server_name` from `"127.0.0.1"` to use `GRADIO_SERVER_NAME` env var (defaults to `"0.0.0.0"`)
- [x] Changed `server_port` to use `GRADIO_SERVER_PORT` env var (defaults to `7860`)
- [x] Already has `mcp_server=True` ✓

**requirements.txt:**
- [x] Removed `sseclient>=0.0.27` (not needed for Gradio 6 native MCP)
- [x] Has `gradio[mcp]>=6.0.0` ✓
- [x] All other dependencies present

---

## 🚀 Deployment Steps

### 1. Create Hugging Face Space

1. Go to: https://huggingface.co/new-space
2. Fill in:
   - **Name:** `gitroast-mcp` (or your choice)
   - **License:** MIT
   - **SDK:** Gradio
   - **Hardware:** CPU Basic (free tier works fine)
   - **Visibility:** Public

### 2. Upload Files to Space

**Option A: Via Web UI**

Upload these files:
- `app.py` ✓ (updated)
- `logic.py` ✓
- `requirements.txt` ✓ (cleaned)
- Rename `README_HF_SPACES.md` to `README.md` ✓

**Option B: Via Git**

```bash
# Add Hugging Face remote
git remote add hf https://huggingface.co/spaces/YOUR_USERNAME/gitroast-mcp

# Push to Hugging Face
git push hf main
```

**Do NOT upload:**
- `.env` (contains secrets!)
- `__pycache__/`
- `.venv/`
- `.git/`
- `docs/` (optional, can include if you want)

### 3. Configure Secrets (Optional but Recommended)

In your Space Settings → Variables and secrets:

Add these as **Secrets** (not Variables):
- `GITHUB_TOKEN` = your GitHub token
- `GEMINI_API_KEY` = your Gemini API key
- `GEMINI_MODEL` = `gemini-2.5-flash-preview-09-2025`

**Why secrets?**
- Users can't see them
- Better security
- Space will use them automatically

### 4. Verify Deployment

Once the Space builds (takes 1-2 minutes):

**Test Web UI:**
- Visit: `https://YOUR_USERNAME-gitroast-mcp.hf.space`
- Enter `facebook/react`
- Click "🔥 Roast This Repo!"
- Should see roast results

**Test MCP Endpoint:**
- MCP endpoint is at: `https://YOUR_USERNAME-gitroast-mcp.hf.space/gradio_api/mcp/`
- Don't test in browser (it will show errors - that's normal)
- Test with Claude Desktop instead

### 5. Connect Claude Desktop to Your Space

Edit `%APPDATA%\Claude\claude_desktop_config.json`:

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

Restart Claude Desktop and test:
```
Use GitRoast to analyze facebook/react
```

---

## 📝 Post-Deployment Updates

### Update Your Main README.md

Add these sections to your main project README:

```markdown
## 🌐 Live Demo

**Try it now:** https://YOUR_USERNAME-gitroast-mcp.hf.space

**MCP Endpoint:** https://YOUR_USERNAME-gitroast-mcp.hf.space/gradio_api/mcp/
```

### Create Demo Video

Record showing:
1. Web interface working
2. Claude Desktop MCP connection
3. Live analysis demo

Upload to YouTube and add link to README.

### Social Media Post

Post on Twitter/LinkedIn with:
- Link to Space
- Link to demo video
- Screenshots
- Hashtags: #MCPFirstBirthday #BuildingMCP

---

## ✅ Verification Checklist

Before submitting to hackathon:

- [ ] Space is public and loading
- [ ] Web UI works (can analyze repos)
- [ ] MCP endpoint exists at `/gradio_api/mcp/`
- [ ] Claude Desktop can connect and use it
- [ ] README has hackathon tags (building-mcp-track-consumer)
- [ ] Demo video recorded and uploaded
- [ ] Social media post published
- [ ] All links in README work
- [ ] No secrets in public code

---

## 🐛 Troubleshooting

### Space won't build

**Check:**
- `requirements.txt` syntax is correct
- `app.py` has no syntax errors
- All imports are available

### MCP endpoint not working

**Verify:**
- `mcp_server=True` in `demo.launch()`
- Space is running (not sleeping)
- Using correct URL with `/gradio_api/mcp/`

### Environment variables not working

**Check:**
- Added as Secrets (not Variables)
- Names match exactly (case-sensitive)
- Space has been restarted after adding secrets

### Rate limit errors

**Solution:**
- Add `GITHUB_TOKEN` secret
- Restart Space

---

## 📊 Key Configuration Details

### Port Configuration
According to [Gradio environment variables documentation](https://www.gradio.app/guides/environment-variables):
- **Default port:** 7860
- **Environment variable:** `GRADIO_SERVER_PORT`
- **Hugging Face Spaces:** Automatically handles port configuration

### Server Name Configuration
- **Local development:** `"127.0.0.1"` (localhost only)
- **Hugging Face Spaces:** `"0.0.0.0"` (all interfaces)
- **Environment variable:** `GRADIO_SERVER_NAME`

Your code now correctly uses:
```python
server_name = os.getenv("GRADIO_SERVER_NAME", "0.0.0.0")
port = int(os.getenv("GRADIO_SERVER_PORT", 7860))
```

This works for both local development and Spaces deployment!

---

## 🎯 Summary

**What changed:**
1. ✅ Updated `app.py` to use environment variables for port/server
2. ✅ Removed `sseclient` from requirements (not needed)
3. ✅ Created `README_HF_SPACES.md` with proper frontmatter

**Ready to deploy:**
- Just upload files to Hugging Face Space
- Add API keys as Secrets (optional)
- Test and verify

**Your app will work on Spaces because:**
- Port configuration is now dynamic ✓
- Server name uses environment variable ✓
- Native Gradio 6 MCP support (no custom bridge) ✓
- All dependencies are available ✓

---

## 📚 Resources

- [How to Build an MCP Server with Gradio](https://huggingface.co/blog/gradio-mcp)
- [Gradio MCP Server Guide](https://www.gradio.app/guides/building-mcp-server-with-gradio)
- [Gradio Spaces Documentation](https://huggingface.co/docs/hub/en/spaces-sdks-gradio)
- [Gradio Environment Variables](https://www.gradio.app/guides/environment-variables)
- [Spaces Configuration Reference](https://huggingface.co/docs/hub/spaces-config-reference)

**You're ready to deploy!** 🚀
