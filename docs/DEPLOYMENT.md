# Deployment Guide

Guide for deploying GitRoast MCP Server to various platforms.

## Hugging Face Spaces (Recommended)

Best for: Public demos, hackathon submissions, easy sharing

### Quick Deploy

1. **Create Space:**
   - Go to https://huggingface.co/spaces
   - Click "Create new Space"
   - Choose Gradio SDK

2. **Upload Files:**
   - `app.py`
   - `logic.py`
   - `requirements.txt`
   - `README.md`

3. **Add Secrets** (in Space Settings):
   - `GITHUB_TOKEN` (optional)
   - `GEMINI_API_KEY` (optional)

4. **Access:**
   - Web UI: `https://YOUR_USERNAME-gitroast-mcp.hf.space`
   - MCP: `https://YOUR_USERNAME-gitroast-mcp.hf.space/gradio_api/mcp/`

### MCP Client Config

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

---

## Local Development

Best for: Testing, development, private use

### Setup

```bash
# Clone and install
git clone https://github.com/your-username/git-roast-mcp.git
cd git-roast-mcp
pip install -r requirements.txt

# Configure
cp .env.example .env
# Edit .env with your API keys

# Run
python app.py
```

### Access

- Web UI: http://127.0.0.1:7860
- MCP: http://127.0.0.1:7860/gradio_api/mcp/

---

## Docker Deployment

Best for: Self-hosting, production, cloud servers

### Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
COPY app.py logic.py ./

# Expose port
EXPOSE 7860

# Set environment variables (optional defaults)
ENV GRADIO_SERVER_NAME=0.0.0.0
ENV GRADIO_SERVER_PORT=7860

# Run application
CMD ["python", "app.py"]
```

### Build and Run

```bash
# Build
docker build -t gitroast-mcp .

# Run
docker run -p 7860:7860 \
  -e GITHUB_TOKEN=your_token \
  -e GEMINI_API_KEY=your_key \
  gitroast-mcp
```

### Docker Compose

```yaml
version: '3.8'

services:
  gitroast:
    build: .
    ports:
      - "7860:7860"
    environment:
      - GITHUB_TOKEN=${GITHUB_TOKEN}
      - GEMINI_API_KEY=${GEMINI_API_KEY}
    restart: unless-stopped
```

Run with: `docker-compose up -d`

---

## Cloud Platforms

### Railway

```bash
# Install Railway CLI
npm install -g @railway/cli

# Deploy
railway login
railway init
railway up
```

Add environment variables in Railway dashboard.

### Render

1. Create new Web Service
2. Connect GitHub repo
3. Build command: `pip install -r requirements.txt`
4. Start command: `python app.py`
5. Add environment variables

### Fly.io

```toml
# fly.toml
app = "gitroast-mcp"

[build]
  builder = "paketobuildpacks/builder:base"

[[services]]
  http_checks = []
  internal_port = 7860
  protocol = "tcp"

  [[services.ports]]
    port = 80
    handlers = ["http"]

  [[services.ports]]
    port = 443
    handlers = ["tls", "http"]
```

Deploy:
```bash
fly launch
fly secrets set GITHUB_TOKEN=your_token
fly secrets set GEMINI_API_KEY=your_key
fly deploy
```

---

## Production Considerations

### Environment Variables

Never hardcode secrets. Always use environment variables:

```python
import os
from dotenv import load_dotenv

load_dotenv()

GITHUB_TOKEN = os.getenv('GITHUB_TOKEN')
GEMINI_API_KEY = os.getenv('GEMINI_API_KEY')
```

### Security

- Use HTTPS in production
- Validate input thoroughly
- Rate limit API calls
- Don't expose internal errors to users
- Keep dependencies updated

### Performance

```python
# In app.py, add:
demo.launch(
    mcp_server=True,
    server_name="0.0.0.0",
    max_threads=10,  # Adjust based on traffic
    show_error=False  # Don't show internal errors
)
```

### Monitoring

Add logging:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

logger = logging.getLogger(__name__)
```

---

## Scaling

### Horizontal Scaling

Use a load balancer with multiple instances:

```
Load Balancer
    ↓
    ├─ Instance 1 (port 7860)
    ├─ Instance 2 (port 7861)
    └─ Instance 3 (port 7862)
```

### Caching

Add caching for GitHub API responses:

```python
from functools import lru_cache

@lru_cache(maxsize=100)
def analyze_repo_cached(url: str):
    return analyze_repo(url)
```

---

## Troubleshooting Deployment

### Port Issues

Make sure your platform allows port 7860, or use environment variable:

```python
import os

port = int(os.getenv('PORT', 7860))
demo.launch(mcp_server=True, server_port=port)
```

### Memory Issues

Reduce workers or use smaller model:

```python
demo.launch(
    mcp_server=True,
    max_threads=4  # Reduce from default
)
```

### Timeout Issues

Increase timeout for slow repos:

```python
# In logic.py
requests.get(url, timeout=60)  # Increase from 30
```

---

## Health Checks

Add a health check endpoint:

```python
@app.get("/health")
def health():
    return {"status": "healthy"}
```

---

## Backup and Recovery

- Keep environment variables in secure vault
- Version control your code
- Regular backups of any custom data
- Document your deployment process

---

## Cost Optimization

### Free Tiers

- Hugging Face Spaces: Free (CPU basic)
- Render: Free (with limitations)
- Railway: $5/month credit free

### Reduce Costs

- Cache API responses
- Rate limit requests
- Use smaller compute instances
- Only run when needed (not 24/7)

---

## Next Steps

- Set up monitoring (Sentry, LogRocket)
- Add analytics (if needed)
- Configure custom domain
- Set up SSL/TLS
- Create backup strategy

---

For hackathon submission, **Hugging Face Spaces** is the easiest and recommended option.
