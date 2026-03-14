---
title: 'Notes on sandboxed coding agents'
description: 'How to setup Claude Code or other coding agents in a secure sandbox'
pubDate: 'Mar 14 2026'
heroImage: './llm-sandbox.png'
---

TLDR;

Build your Claude Code image with Docker:

```
FROM node:20-slim

# Create a non-root user for safer execution
RUN useradd -m -u 1001 claude

# Install Claude Code CLI globally
RUN npm install -g @anthropic-ai/claude-code

# Set the working directory
WORKDIR /workspace

# Switch to non-root user
USER claude

ENTRYPOINT ["claude"]
```

Then run it, binding local credentials to it (optional)

```
docker run -it --rm \
  -v ~/.claude:/home/claude/.claude \
  -v ~/.claude.json:/home/claude/.claude.json \
  -v $(pwd):/workspace \
  claude-code:latest --dangerously-skip-permissions
```

Thats it! I recommend setting up some kind of alias for this, eg `xclaude` - that is more convenient.
