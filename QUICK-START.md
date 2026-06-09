# 🚀 Quick Start: Unlimited Free AI Coding in 5 Minutes

Choose your path below and follow the steps. **No credit card required.**

---

## ⚡ Path 1: Instant Setup (5 min) - Cloud Tools Only

**Best for**: Everyone who wants instant results

### Step 1: Install One CLI Tool (2 min)
```bash
# macOS
brew install ollama  # For local models (optional but recommended)

# Windows/Linux
# Download from: https://ollama.ai/download
```

### Step 2: Get Free API Keys (2 min)
Choose ANY of these (pick your favorite):

**Option A: Qwen Code** (2,000 requests/day)
```bash
# Install
pip install qwen-code

# Run (opens browser for login)
qwen --version
qwen "Write a Python hello world"
```
→ Link: https://github.com/QwenLM/qwen-code

**Option B: GitHub Copilot** (50 chats/month)
```bash
# Already built-in if you use VS Code
# Just enable in VSCode settings
```
→ Link: https://github.com/features/copilot/plans

**Option C: Gemini CLI** (100 requests/day)
```bash
pip install gemini-cli
gemini auth login
gemini "Write a FastAPI server"
```
→ Link: https://github.com/google-gemini/gemini-cli

### Step 3: Start Coding (1 min)
```bash
# Example with Qwen
qwen "Create a React component for a todo list"

# Example with Gemini
gemini "Optimize this Python code for performance"

# Example with GitHub Copilot
# Use Cmd+K in VS Code
```

✅ **Done!** You now have ~2,000+ free requests/day

---

## 💻 Path 2: Best Setup (20 min) - Local + Cloud

**Best for**: Developers who want unlimited capacity + control

### Step 1: Install Local AI (10 min)
```bash
# 1. Install Ollama
brew install ollama  # macOS
# Windows/Linux: https://ollama.ai/download

# 2. Download a powerful model (takes 5-10 min, runs once)
ollama pull qwen2.5-coder:32b  # ~20GB, very smart

# 3. Start the server (runs in background)
ollama serve
# Server ready at http://localhost:11434
```

### Step 2: Connect to VS Code (5 min)
```bash
# 1. Install Continue.dev extension
#    - Open VS Code → Extensions → Search "Continue"
#    - Click Install

# 2. Create config file
# macOS/Linux:
mkdir -p ~/.continue
cat > ~/.continue/config.json << 'EOF'
{
  "models": [
    {
      "title": "Qwen Local (Free)",
      "provider": "ollama",
      "model": "qwen2.5-coder:32b"
    }
  ],
  "tabAutocompleteModel": {
    "provider": "ollama",
    "model": "qwen2.5-coder:32b"
  }
}
EOF

# Windows:
# Open: C:\Users\YourName\AppData\Roaming\Continue
# Create config.json (same content above)
```

### Step 3: Try It (1 min)
```
1. Open a file in VS Code
2. Press Cmd+K (Mac) or Ctrl+K (Windows)
3. Type: "Write a function to validate email"
4. See AI response instantly (runs on your machine!)
```

✅ **Done!** You now have unlimited AI coding + Copilot backup

---

## 🏆 Path 3: Maximum Free Capacity (30 min) - Full Stack

**Best for**: Power users who want infinite requests

### Setup (follow all 3 paths above, then add these):

**Step 1: Add Rovo Dev CLI** (5M tokens/day!)
```bash
# Requires Atlassian account (free tier available)
# https://support.atlassian.com/rovo/docs/use-rovo-dev-cli/

# Install & authenticate
brew install rovo-dev-cli
rovo login

# Use it
rovo "Refactor this code for readability"
```

**Step 2: Add Gemini CLI** (100 requests/day)
```bash
pip install google-generativeai
gemini auth login
gemini "Create database schema for blog"
```

**Step 3: Add Jules** (15 tasks/day)
```bash
# No install needed - use web interface
# https://jules.google/
```

**Step 4: Setup Automation Script** (5 min)
```bash
# Create rotate.sh
cat > ~/rotate.sh << 'EOF'
#!/bin/bash

TOOLS=("qwen" "gemini" "rovo")
TODAY=$(date +%u)
TOOL_INDEX=$((($TODAY - 1) % 3))
CURRENT_TOOL=${TOOLS[$TOOL_INDEX]}

echo "Today's primary tool: $CURRENT_TOOL"

case $CURRENT_TOOL in
  qwen)
    echo "Using: Qwen Code (2,000 req/day)"
    ;;
  gemini)
    echo "Using: Gemini CLI (100 req/day)"
    ;;
  rovo)
    echo "Using: Rovo Dev (5M tokens/day)"
    ;;
esac
EOF

chmod +x ~/rotate.sh
~/rotate.sh
```

✅ **Done!** You now have ~10M+ tokens/day for free

---

## 📊 What You Now Have

| Setup | Capacity | Setup Time | Cost |
|-------|----------|-----------|------|
| **Path 1** | 2K+ requests/day | 5 min | $0 |
| **Path 2** | ∞ (local) | 20 min | $0 |
| **Path 3** | 5M+ tokens/day | 30 min | $0 |
| **All Combined** | **Unlimited** | 30 min | **$0** |

---

## 🎯 Common Commands

### Using Qwen Code
```bash
qwen "Write a REST API endpoint"
qwen "Debug this error: [paste error]"
qwen "Explain what this code does" < file.py
```

### Using Gemini CLI
```bash
gemini "Convert this curl to Python requests"
gemini -m "gemini-2.5-pro" "Advanced analysis task"
```

### Using VS Code + Continue.dev
```
Cmd+K (Mac) or Ctrl+K (Windows)  → Ask AI
Cmd+L (Mac) or Ctrl+L (Windows)  → Edit code
Cmd+I (Mac) or Ctrl+I (Windows)  → Quick fix
```

### Using Ollama Directly
```bash
# Direct API call
curl http://localhost:11434/api/generate \
  -d '{
    "model": "qwen2.5-coder:32b",
    "prompt": "Write Python code for quicksort",
    "stream": false
  }'
```

---

## 🔧 Troubleshooting

### "Command not found: qwen"
```bash
# Make sure Python is installed
python3 --version

# Reinstall
pip install qwen-code
```

### "Ollama connection refused"
```bash
# Make sure Ollama server is running
ollama serve

# In another terminal, test:
curl http://localhost:11434/api/tags
```

### "VS Code can't find Continue.dev"
```bash
# Restart VS Code after installing extension
# Mac: Cmd+Q then reopen
# Windows: Alt+F4 then reopen
```

### "Model download is slow"
```bash
# This is normal - first download takes 5-10 min
# Leave running and grab coffee ☕
# Download only happens once
```

---

## 💡 Pro Tips

### Tip 1: Combine Tools
```bash
# Check quota for today
qwen --status

# If limit reached, switch to Gemini
gemini "Same question here"

# If both full, use local Ollama (unlimited)
# In VS Code: Cmd+K
```

### Tip 2: Use for Different Tasks
```bash
# Quick syntax questions → Qwen (fast)
qwen "What's the Python syntax for..."

# Complex analysis → Rovo (5M tokens, better for long contexts)
rovo "Analyze this architecture..."

# UI/Frontend → Gemini (excellent for frontend)
gemini "Design a responsive header component"

# Unlimited work → Local Ollama (no limits)
# Use in VS Code for continuous coding
```

### Tip 3: Save API Calls
```bash
# ❌ Bad - uses 1 request
qwen "Write a function"

# ✅ Good - uses 1 request, gives more context
qwen "Write a function that:
- Takes array of objects
- Filters by price > 100
- Returns sorted by date
- Include tests"
```

### Tip 4: Use Local First
```bash
# In VS Code, set Ollama as primary:
# Continue.dev settings → Ollama as default

# Why? 
# - No API limits
# - Faster feedback
# - Works offline
# - Cloud tools as backup
```

---

## 🚀 Next Steps

1. **Choose your path** (1, 2, or 3 above)
2. **Follow the setup** (5-30 minutes)
3. **Start coding** with AI
4. **Share with friends** → https://github.com/estebouza/free-ai-coding

---

## ❓ Still Have Questions?

- **Qwen Code**: https://github.com/QwenLM/qwen-code
- **Continue.dev**: https://www.continue.dev/docs
- **Ollama**: https://github.com/ollama/ollama
- **GitHub Copilot**: https://docs.github.com/en/copilot
- **Full Guide**: See README.md

---

## 📱 One-Liner Installations

### macOS - Install Everything
```bash
brew install ollama && \
pip install qwen-code gemini-cli && \
echo "✅ All tools installed! Run: ollama pull qwen2.5-coder:32b"
```

### Linux - Install Everything
```bash
curl https://ollama.ai/install.sh | sh && \
pip install qwen-code gemini-cli && \
echo "✅ All tools installed!"
```

### Windows - Install Everything
```powershell
# Download Ollama: https://ollama.ai/download
# Then in PowerShell:
pip install qwen-code gemini-cli
# Done!
```

---

**Ready? Start with Path 1 above and code in 5 minutes!** 🎉
