Last updated: December 9, 2025 • PRs/issues welcome

**Languages:** [Español](README-es.md) • [Português](README-pt-BR.md) • [中文](README-zh.md) • [Français](README-fr.md) • [日本語](README-ja.md) • [हिन्दी](README-hi.md)

# AI Coding Tools: Where Pro-Grade Models Are Actually Free 

Many AI coding tools claim to be "free," but access to pro-grade models usually runs out fast, then you're downgraded. Each tool uses different limits (credits, tokens, requests), making comparison challenging.

---

## 🚀 NEW: The Ultimate Guide to Unlimited Free AI Coding

**TL;DR**: Don't use just one tool—stack multiple free tiers together for **virtually unlimited access**.

### Strategy #1: Combine Multiple Free Tools (Recommended)
Rotate between tools with high daily/monthly limits:

| Tool | Daily/Monthly Limit | Model | Reset |
|------|-------------------|-------|-------|
| **Qwen Code** | 2,000 requests/day | Qwen3-Coder-480B | Daily 00:00 UTC |
| **Rovo Dev CLI** | 5M tokens/day | Claude Sonnet 4 | Daily 00:00 UTC |
| **Gemini CLI** | 100 requests/day | Gemini 2.5 Pro | Daily 00:00 UTC |
| **GitHub Copilot** | 50 chats/month | GPT-4.1, Claude Opus | Monthly |
| **Jules** | 15 tasks/day | Gemini 2.5 Pro | Rolling 24h |

**Monthly Capacity**: ~5.2 million tokens/day + unlimited other requests = **158M+ tokens/month free**

```bash
# Pseudo-setup for daily rotation
Day 1: Qwen Code (2,000 req) → Rovo CLI (5M tokens)
Day 2: Gemini CLI (100 req) → GitHub Copilot (chat)
Day 3: Jules (15 tasks) → Cycle back to Qwen
```

**Why This Works**: Different tools reset at different times. Stacking them gives you ~5-10x more capacity than any single tool.

---

### Strategy #2: Local Models (Truly Unlimited, No Resets)
Run frontier models on your hardware—zero API limits, zero costs after setup.

**Quick Start**:
```bash
# Install Ollama (macOS/Linux/Windows)
brew install ollama  # macOS
# or: https://ollama.ai/download

# Download a powerful coding model (one-time download)
ollama pull qwen2.5-coder:32b    # ~20GB, very good
ollama pull mistral:latest        # ~10GB, lightweight
ollama pull llama2-uncensored:70b # ~40GB, best chat

# Use with VS Code extension (Continue.dev)
# Configure in .continue/config.json:
# "provider": "ollama", "model": "qwen2.5-coder:32b"
```

**Pros**:
- ✅ Infinite requests (limited by your hardware)
- ✅ No API keys needed
- ✅ Complete privacy
- ✅ Works offline

**Cons**:
- ⚠️ Requires 20-150GB disk/RAM
- ⚠️ Slower than cloud (but still fast with good hardware)
- ⚠️ GPU recommended for speed

**Recommended Setup**:
- **Minimum**: Qwen2.5-Coder-32B (20GB, ~100 tokens/sec)
- **Optimal**: Qwen2.5-Coder-32B + Mistral (30GB total)
- **Best**: Qwen2.5-Coder-32B + Deepseek-v3 (needs 150GB+)

---

### Strategy #3: API Providers with High Free Tiers
Use provider APIs that compatible with Continue.dev, Cline, Cursor:

| Provider | Free Tier | Setup Time |
|----------|-----------|-----------|
| [OpenRouter](https://openrouter.ai/) | 50 req/day (1K if $10+ spent) | 2 min |
| [Cerebras](https://cloud.cerebras.ai/) | 1M tokens/day | 2 min |
| [Together AI](https://www.together.ai/) | Generous free tier | 2 min |

```bash
# Example with Continue.dev + Cerebras (1M free tokens/day)
1. Sign up at https://cloud.cerebras.ai/ (no card needed)
2. Get API key from dashboard
3. Add to .continue/config.json:
   {
     "provider": "cerebras",
     "apiKey": "YOUR_KEY",
     "model": "qwen3-235b"
   }
```

---

### Strategy #4: Create a Proxy Automation Script
**Advanced**: Automatically rotate between tools when one hits its limit:

```python
#!/usr/bin/env python3
# ai_unlimited.py - Auto-rotate between free tools

import os
from datetime import datetime, timedelta

TOOLS = {
    "qwen": {
        "limit": 2000,
        "reset": "daily",
        "provider": "qwen-oauth",
        "used": 0
    },
    "rovo": {
        "limit": 5_000_000,  # tokens
        "reset": "daily",
        "provider": "atlassian",
        "used": 0
    },
    "gemini": {
        "limit": 100,
        "reset": "daily",
        "provider": "google-oauth",
        "used": 0
    }
}

def get_available_tool():
    """Return next tool with available quota"""
    for tool, config in TOOLS.items():
        if config["used"] < config["limit"]:
            return tool
    return None  # All tools exhausted

def request_ai(prompt, model_preference="best"):
    """Route request to available tool"""
    tool = get_available_tool()
    if not tool:
        print("⚠️ All free tiers exhausted today. Try again tomorrow!")
        return None
    
    print(f"✅ Using {tool}...")
    response = submit_to_tool(tool, prompt)
    TOOLS[tool]["used"] += 1
    return response

# Example usage
if __name__ == "__main__":
    prompt = "Write a FastAPI server with authentication"
    result = request_ai(prompt)
    print(result)
```

**Better yet**: Check out existing projects like [CLIProxyAPI](https://github.com/estebouza/CLIProxyAPI) which does this already.

---

### Strategy #5: Account Multiplication (For Teams)
- Create separate GitHub accounts → each gets Copilot free tier
- Create separate Google accounts → each gets Jules + Gemini free tier
- Use personal + work + side-project emails → 3x the quota

**⚠️ Ethical Note**: This technically works but violates most TOS. Use only for personal projects or with organizational approval.

---

## 💰 Cost Comparison: Unlimited Access

| Method | Setup | Monthly Cost | Unlimited? |
|--------|-------|-------------|-----------|
| Stack 5 free tools | 1 hour | $0 | ✅ Yes (5M+ tokens) |
| Local Qwen-32B | 2 hours + disk | $0 (hardware) | ✅ Yes |
| Cerebras 1M tokens/day | 5 min | $0 | ✅ 30M/month |
| Trae Pro + Copilot | 5 min | $20 | ✅ Yes |
| Claude Pro | - | $20 | ✅ 200K tokens/month |
| GPT-4o Pro + Copilot | - | $50 | ✅ Yes |

**Winner**: **Stack free tools + Ollama local** = $0, unlimited capacity, zero waiting.

---

## ⚙️ Recommended Setup for Maximum Free Capacity

### **Tier 1: Free Stack (Recommended)**
```bash
# 1. Install all CLI tools (1 hour setup)
brew install ollama                # Local models
pip install qwen-code              # Qwen CLI
pip install gemini-cli             # Gemini CLI
brew install --cask cursor         # Editor (free until Dec 11)
brew install warp                  # Terminal with AI (75 credits/month)

# 2. Create API keys (15 min)
# - GitHub: https://github.com/settings/tokens
# - Google: console.cloud.google.com
# - Atlassian: developer.atlassian.com
# - Alibaba: https://qwen.aliyun.com

# 3. Configure your editor (.continue/config.json)
# {
#   "models": [
#     { "provider": "ollama", "model": "qwen2.5-coder:32b" },
#     { "provider": "gemini", "model": "gemini-2.5-pro" },
#     { "provider": "github-copilot" }
#   ]
# }

# Result: Unlimited local + 2K+ daily requests = Effectively infinite
```

### **Tier 2: Premium Setup ($20/month)**
- Trae Pro ($10/mo) → 600 fast requests + unlimited slow
- GitHub Copilot Pro ($10/mo) → 300 chat + unlimited completions
- **Total**: 900 fast requests + unlimited slow + 5M Qwen daily

### **Tier 3: Enterprise ($50+/month)**
- Claude Pro ($20/mo)
- GPT-4o Pro ($20/mo) 
- GitHub Copilot Pro ($10/mo)
- AWS Kiro Pro ($20/mo)

---

## 🔗 Integration Examples

### Cursor + Ollama (Unlimited local)
```json
// .cursor/cursor_settings.json
{
  "models": {
    "claude": { "provider": "ollama", "model": "qwen2.5-coder:32b" },
    "gpt4": { "provider": "ollama", "model": "deepseek-v3" }
  }
}
```

### VS Code + Continue.dev (Multi-provider)
```json
// .continue/config.json
{
  "models": [
    {
      "title": "Local (Fast)",
      "provider": "ollama",
      "model": "qwen2.5-coder:32b"
    },
    {
      "title": "Gemini (Free 100/day)",
      "provider": "gemini",
      "model": "gemini-2.5-pro"
    },
    {
      "title": "Copilot (Free 50/month)",
      "provider": "github-copilot"
    }
  ]
}
```

---

## TL;DR — Free Tiers for Pro‑Grade AI Coding
(tools with higher limits listed first)

| Tool | Pro‑grade models | Free tier limit | Credit card |
|------|------------------|------------------|-------------|
| [Qwen Code](https://github.com/QwenLM/qwen-code) | Qwen3-Coder-480B | 2,000 requests/day | No |
| [Rovo Dev CLI](https://www.atlassian.com/blog/announcements/rovo-dev-command-line-interface) | Claude Sonnet 4 | 5M tokens/day (beta) | No |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Gemini 3 Pro, Gemini 2.5 Pro | Gemini 3 Pro (waitlist/paid), 100 req/day Gemini 2.5 Pro | No |
| [Cursor](https://cursor.com/) | GPT-5.1-Codex-Max | Free until Dec 11, 2025 (77.9% SWE-bench) | No |
| [Kilo Code](https://kilocode.ai/) | Claude Opus/Sonnet, Gemini 2.5 Pro, GPT‑4.1 | Up to $25 signup credits (one‑time) | Yes |
| [Warp](https://warp.dev/) | GPT‑5, Claude Opus 4.1, Claude Sonnet 4, Gemini 2.5 Pro | 150 credits/month (first 2 months), then 75/month | No |
| [Trae](https://trae.ai/) | Claude 4 Sonnet (Beta), Claude 3.7 Sonnet, GPT‑4.1, GPT‑4o, Gemini 2.5 Pro | 10 fast + 50 slow requests/month | No |
| [Amazon Q Developer](https://aws.amazon.com/q/developer/) | Claude Sonnet 4 | 50 agentic requests/month | Yes |
| [GitHub Copilot](https://github.com/features/copilot/plans) | GPT‑4.1, Claude Opus 3.5, Gemini 2.0 Flash, Grok Code Fast 1 | 50 chat requests + 2,000 completions/month | No |
| [Windsurf](https://windsurf.com/) | OpenAI, Anthropic, Google, xAI | 25 credits/month | Yes |
| [Jules](https://jules.google/) | Gemini 2.5 Pro | 15 tasks/day | No |
| [AWS Kiro](https://kiro.dev/) | Claude 4 Sonnet, Claude 3.7 Sonnet | 50 credits/month | No |
| [Qoder](https://qoder.com/) | Qwen3-Coder-480B, Claude, GPT, Gemini | Free tier + 2-week Pro trial (1,000 credits) | No |

### Qualifying Pro‑Grade Models
Only models achieving >60% on SWE-bench Verified qualify as pro-grade for real-world coding tasks. Below is the current list

| Model | SWE-bench Verified | Provider |
|-------|-------------------|----------|
| Claude Opus 4.5 | 80.9% | Anthropic |
| GPT-5.1-Codex-Max | 77.9% | OpenAI |
| Claude Sonnet 4.5 | 77.2% (82.0% w/ parallel) | Anthropic |
| Gemini 3 Pro | 76.2% | Google |
| GPT-5 | 74.9% | OpenAI |
| Claude Opus 4.1 | 74.5% | Anthropic |
| Claude Sonnet 4 | 72.7% (80.2% w/ parallel) | Anthropic |
| GPT-5 mini | 71.0% | OpenAI |
| Qwen3-Coder-480B | 69.6% (interactive) / 67.0% (single) | Alibaba |
| Gemini 2.5 Pro | 63.2% | Google |

### Contributing

If you spot an error, missing source link, or have updated quota/model information, please open an issue or pull request with a source. New tool contributions are welcomed! See CONTRIBUTING.md for guidelines.

### Disclaimer

No affiliation with any vendor. All trademarks belong to their owners. Information is for research; accuracy not guaranteed; limits/pricing change frequently.

## Contents

- [🚀 The Ultimate Guide to Unlimited Free AI Coding](#-the-ultimate-guide-to-unlimited-free-ai-coding)
- [1. AI-coding Tools with Free Access to Pro-Grade Models](#1-ai-coding-tools-with-free-access-to-pro-grade-models)
- [2. API Providers for AI Coding Tools](#2-api-providers-for-ai-coding-tools)
- [3. Tools with Paid Tiers with Pro-Grade Models](#3-tools-with-paid-tiers-with-pro-grade-models)
- [4. Tools with Free Access to Basic Models](#4-tools-with-free-access-to-basic-models)
- [5. Local Models](#5-local-models)
- [Comparison Notes](#comparison-notes)
- [Related Resources](#related-resources)

## 1. AI-coding Tools with Free Access to Pro-Grade Models
_(ordered from most generous to least)_

### [Qwen Code](https://github.com/QwenLM/qwen-code)

> **Qwen3-Coder-480B access**
- 2,000 requests/day free tier via Qwen OAuth
- 60 requests/minute rate limit
- Command-line AI workflow tool (adapted from Gemini CLI)
- One-click browser authentication
- No credit card required

**** [GitHub](https://github.com/QwenLM/qwen-code) | [Documentation](https://github.com/QwenLM/qwen-code#readme)

---

### [Rovo Dev CLI](https://www.atlassian.com/blog/announcements/rovo-dev-command-line-interface)

> **Claude Sonnet 4 access during beta**
- 5M tokens/day free tier (20M on first day only)
- Claude Sonnet 4 model (confirmed via testing)
- No credit card required during beta
- Token limits reset at midnight UTC
- Note: Upgrade to Jira Standard/Premium/Enterprise for 20M tokens/day

**** [Documentation](https://support.atlassian.com/rovo/docs/use-rovo-dev-cli/) | [Token Limits](https://support.atlassian.com/rovo/docs/rovo-dev-cli-limits/)

---

### [Gemini CLI](https://github.com/google-gemini/gemini-cli)

> **Gemini 3 Pro and Gemini 2.5 Pro access**
- Gemini 3 Pro now available (Dec 4, 2025) for Google AI Ultra subscribers and paid API users
- Gemini 3 Pro: 76.2% SWE-bench Verified — Google's best coding model
- 100 requests/day limit for Gemini 2.5 Pro (free tier fallback)
- 250 requests/day limit for Gemini 2.5 Flash
- No credit card required for free tier
- Waitlist for Gemini 3 Pro access for Google AI Pro, Gemini Code Assist standard, and free tier users
- Enable via `/settings` → Preview features → true

**** [Rate Limits](https://ai.google.dev/gemini-api/docs/rate-limits) | [Pricing](https://ai.google.dev/gemini-api/docs/pricing) | [Gemini 3 Pro Announcement](https://developers.googleblog.com/en/gemini-3-pro-is-here/)

---

### [Kilo Code](https://kilocode.ai/)

> **Claude Opus/Sonnet, Gemini 2.5 Pro, GPT-4.1 access**
- Up to $25 signup credits (one-time bonus)
- Open source VS Code extension
- Pay-as-you-go with no markup on model pricing
- Credit card required to claim full bonus credits
- Supports bringing your own API keys

**** [GitHub](https://github.com/Kilo-Org/kilocode) | [Documentation](https://kilocode.ai/docs/) | [Pricing](https://kilocode.ai/pricing)

---

### [Warp](https://warp.dev/)

> **GPT‑5, Claude Opus 4.1, Claude Sonnet 4, Gemini 2.5 Pro access**
- 150 AI credits/month (first 2 months), then 75 AI credits/month
- Multiple providers (OpenAI GPT‑5, Claude Opus 4.1, Claude Sonnet 4, Gemini 2.5 Pro)
- No credit card required for basic signup
- New pricing structure announced Oct 30, 2025: Single Build plan ($20/mo) with 1,500 credits

**** [Pricing](https://www.warp.dev/pricing)

---

### [Amazon Q Developer](https://aws.amazon.com/q/developer/)

> **Claude Sonnet 4 access**
- 50 agentic requests/month limit (multi-turn conversations)
- Latest Claude models (AWS-hosted)
- Credit card required
- Must upgrade to Pro for continued access
- Perpetual free tier

**** [Pricing](https://aws.amazon.com/q/developer/pricing/)

---

### [GitHub Copilot](https://github.com/features/copilot/plans)

> **Agent Mode with GPT‑4.1, Claude Opus 3.5, Gemini 2.0 Flash, Grok Code Fast 1**
- 50 chat requests + 2,000 completions/month limit
- Agent Mode with autonomous multi-step coding
- Multiple providers (GPT-4.1, Claude Opus 3.5, Gemini 2.0 Flash, Grok Code Fast 1)
- No credit card required
- Limited to basic features after quota

**** [Plans Details](https://docs.github.com/en/copilot/get-started/plans-for-github-copilot) | [Agent Mode](https://code.visualstudio.com/blogs/2025/02/24/introducing-copilot-agent-mode)

---

### [Trae](https://trae.ai/)

> **Claude 4 Sonnet (Beta), Claude 3.7 Sonnet, Claude 3.5 Sonnet, GPT‑4.1, GPT‑4o, Gemini 2.5 Pro access**
- 10 fast requests + 50 slow requests/month for premium models
- 1,000 slow requests/month for advanced models
- 5,000 auto-completions/month
- VS Code-based IDE with AI integration
- Multiple premium models including Claude 4 Sonnet (Beta), Claude 3.7 Sonnet, GPT‑4.1
- No credit card required for free tier
- Pro Plan: $10/mo (600 fast + unlimited slow requests)

**** [Pricing](https://trae.ai/pricing) | [Documentation](https://docs.trae.ai/ide/billing)

---

### [Windsurf](https://windsurf.com/)

> **OpenAI, Anthropic, Google, xAI model access**
- 25 prompt credits/month limit
- Multiple providers (OpenAI, Claude, Gemini, xAI)
- Credit card required
- Can purchase add-on credits to continue

**** [Pricing](https://windsurf.com/pricing)

---

### [Jules](https://jules.google/)

> **Gemini 2.5 Pro access**
- 15 tasks/day free tier
- 3 concurrent tasks
- Gemini 2.5 Pro model
- Gmail account required (18+ years)
- Task limits reset on rolling 24-hour window
- No credit card required
- Pro tier ($19.99/mo): 100 tasks/day (5x limits)

**** [Usage Limits](https://jules.google/docs/usage-limits/) | [Documentation](https://jules.google/docs/)

---

### [AWS Kiro](https://kiro.dev/)

> **Claude 4 Sonnet, Claude 3.7 Sonnet access**
- 50 credits/month (Free tier)
- Claude 4 Sonnet and Claude 3.7 Sonnet models (AWS-hosted)
- No credit card required
- 14-day welcome bonus: 500 credits
- Paid tiers: Pro ($20/mo - 1,000 credits), Pro+ ($40/mo - 2,000 credits), Power ($200/mo - 10,000 credits)

**** [Pricing](https://kiro.dev/pricing/) | [Introduction Blog](https://kiro.dev/blog/introducing-kiro/)

---

### [Qoder](https://qoder.com/)

> **Qwen3-Coder-480B, Claude, GPT, Gemini models**
- Free tier: Unlimited completions/edits + limited chat/agent requests + 2-week Pro trial (1,000 credits)
- AI-powered IDE from Alibaba
- Available for Windows and macOS
- Primarily uses Qwen3-Coder-480B (Alibaba's flagship coding model)
- Also supports Claude, GPT-4, Gemini models
- Agent Mode and Quest Mode for autonomous coding
- No credit card required (free tier)
- Paid tiers: Pro ($20/mo - 2,000 credits), Pro+ ($60/mo - 6,000 credits)

**** [Homepage](https://qoder.com/) | [Pricing](https://qoder.com/pricing)

Limits change fast. If you see a mistake, a newer quota/model, or want to add a new tool, open an issue or PR with a source. See CONTRIBUTING.md for guidelines.

---

## 2. API Providers for AI Coding Tools
_(ordered from most generous to least)_

These services provide API access to coding-optimized models that integrate with popular AI coding tools like Cursor, Continue.dev, Cline, and others. They don't provide standalone coding tools but enable flexible integrations.

### [OpenRouter](https://openrouter.ai/)

> **Qwen3-Coder-480B via OpenRouter**
- 50 requests/day free tier (1,000/day if purchased $10+ credits)
- Additional free models: Qwen3-30B-A3B, Qwen3-235B-A22B, Gemini Flash
- OpenAI-compatible API for all major IDEs
- No credit card required for free models
- 20 requests/minute rate limit for free tier
- Works with Continue.dev, Cline, Cursor, etc.

**** [Free Models](https://openrouter.ai/models/?q=free) | [Qwen3-Coder API](https://openrouter.ai/qwen/qwen3-coder:free/api)

---

### [Cerebras](https://cloud.cerebras.ai/)

> **Qwen3-235B and Llama 3.1 access**
- Free tier: 1M tokens/day
- No credit card required
- Rate limit: 30 requests/minute, 8,192 token context
- Models: Qwen3-235B, Llama 3.1 70B (Note: Qwen3-Coder-480B deprecated Nov 5, 2025)
- OpenAI-compatible API (works with Cursor, Continue.dev, Cline, RooCode, etc.)
- Ultra-fast inference: 2,000 tokens/second (40x faster than typical providers)
- **Paid tiers:** Developer ($10+ self-serve), Enterprise (custom pricing)

**** [Pricing](https://www.cerebras.ai/pricing) | [API Docs](https://inference-docs.cerebras.ai/) | [Integration Guides](https://inference-docs.cerebras.ai/integrations/)

---

## 3. Tools with Paid Tiers with Pro-Grade Models


### [Rovo Dev CLI](https://www.atlassian.com/blog/announcements/rovo-dev-command-line-interface)

> **Jira Standard ($7.53/user/mo):** 20M tokens/day
- **Jira Premium ($15.25/user/mo):** 20M tokens/day
- **Jira Enterprise (custom):** 20M tokens/day
- 4x increase from free tier (5M → 20M tokens/day)
- Same Claude-based model as free tier
- Token limits reset at midnight UTC

**** [Documentation](https://support.atlassian.com/rovo/docs/use-rovo-dev-cli/) | [Token Limits](https://support.atlassian.com/rovo/docs/rovo-dev-cli-limits/) | [Jira Pricing](https://www.atlassian.com/software/jira/pricing)

---

### [Claude Code](https://www.anthropic.com/claude-code)

> **Pro ($20/mo or $17/mo annually):** Sonnet 4 access with more usage than free tier
- **Max 5x ($100/mo):** ~225 messages/5 hours — 140–280h Sonnet 4 + 15–35h Opus 4.5 weekly
- **Max 20x ($200/mo):** ~900 messages/5 hours — 240–480h Sonnet 4 + 24–40h Opus 4.5 weekly
- Extended thinking modes: "think" (~4K tokens), "megathink" (~10K), "ultrathink" (~32K)
- Ultrathink enables complex refactors, system architecture, and deep debugging
- Opus 4.5 consumes ~5x more resources than Sonnet 4
- Usage limits reset weekly with 5-hour rolling windows
- Works with Opus 4.5, Sonnet 4.5, and Haiku 4.5 models

**** [Pricing](https://www.anthropic.com/pricing) | [Claude Code Guide](https://docs.anthropic.com/en/docs/claude-code)

---

### [Amazon Q Developer](https://aws.amazon.com/q/developer/)

> **Pro ($19/mo):** Increased limits for agentic requests
- Usage may be adjusted based on regional factors and usage patterns

**** [Pricing](https://aws.amazon.com/q/developer/pricing/)

---

### [Warp](https://warp.dev/)

> **Build ($20/mo):** 1,500 AI credits/month
- Reload Credits available (up to 50% cheaper than old overage rates, roll over for 12 months)
- Bring Your Own API Key (BYOK) option available
- New pricing effective immediately for new customers (Oct 30, 2025)
- Existing monthly subscribers transition on first renewal after Dec 1, 2025
- Enterprise tier: Custom pricing

**** [Pricing](https://www.warp.dev/pricing)

---

### [GitHub Copilot](https://github.com/features/copilot/plans)

> **Pro ($10/mo):** 300 premium requests + unlimited completions/month
- **Pro+ ($39/mo):** 1,500 premium requests + unlimited completions/month
- **Business ($19/user/mo):** 300 premium requests + unlimited completions/user/month
- **Enterprise ($39/user/mo):** 1,000 premium requests + unlimited completions/user/month
- **GPT-5.1-Codex-Max** now available in public preview (Dec 4, 2025) for Pro, Pro+, Business, Enterprise
- Access to multiple models (GPT-5.1-Codex-Max, GPT-4.1, Claude Opus 3.5, Gemini 2.0 Flash, Grok Code Fast 1)
- Overage billing available at $0.04/request

**** [Plans Details](https://docs.github.com/en/copilot/get-started/plans-for-github-copilot) | [GPT-5.1-Codex-Max Preview](https://github.blog/changelog/2025-12-04-openais-gpt-5-1-codex-max-is-now-available-to-github-copilot-pro-subscribers/)

---

### [Trae](https://trae.ai/)

> **Pro ($10/mo):** 600 fast requests + unlimited slow requests for premium models
- Unlimited slow requests for advanced models
- Zero rate limits and faster access to premium models
- Extra packages available: $3-$12 for additional fast requests
- Multiple premium models: Claude 4 Sonnet (Beta), Claude 3.7 Sonnet, Claude 3.5 Sonnet, Gemini 2.5 Pro, GPT‑4.1, GPT‑4o
- VS Code-based IDE with full AI integration
- First month available for $3

**** [Pricing](https://trae.ai/pricing) | [Documentation](https://docs.trae.ai/ide/billing)

---

### [Windsurf](https://windsurf.com/)

> **Pro ($15/mo):** 500 prompt credits/month
- **Teams ($30/user/mo):** 500 prompt credits/user/month
- **Enterprise ($60+/user/mo):** 1,000 prompt credits/user/month

**** [Pricing](https://windsurf.com/pricing)

---

### [Lovable](https://lovable.dev/)

> **Pro ($25/mo):** 150 credits/month (5 daily credits)
- **Teams ($30/mo):** Higher limits (undisclosed)

**** [Messaging Limits](https://docs.lovable.dev/user-guides/messaging-limits)

---

### [Bolt.new](https://bolt.new/)

> **$20/mo:** 10M tokens/month
- **$200/mo:** 120M tokens/month

**** [Token Documentation](https://support.bolt.new/account-and-subscription/tokens)

---

### [Cursor](https://cursor.com/)

> **Hobby (Free):** Limited Agent requests + Limited Tab completions + 1-week Pro trial
- **Pro ($20/mo or $16/mo annually):** Extended Agent limits + Unlimited Tab completions + Background Agents + Maximum context windows
- **Pro+ ($60/mo):** 3x usage on all OpenAI, Claude, Gemini models
- **Ultra ($200/mo):** 20x usage on all OpenAI, Claude, Gemini models + Priority access to new features
- **Teams ($40/user/mo):** Pro features + Centralized billing + Usage analytics + SAML/OIDC SSO
- **Enterprise (Custom):** Everything in Teams + Pooled usage + SCIM + AI code tracking API + Audit logs
- **GPT-5.1-Codex-Max free for all users until Dec 11, 2025** (77.9% SWE-bench Verified)
- One-week Pro trial available (free tier)
- Free tier now uses token-based usage tracking (not request-based)
- Free models: Cursor Small, Deepseek v3, Gemini 2.5 Flash, GPT-4o mini (500/day limit), Grok 3 Mini Beta
- Paid tiers: Access to OpenAI, Claude, Gemini models including GPT-5.1-Codex-Max
- Note: Claude models removed from free tier ~June 2025
- AI-powered code editor with autonomous coding capabilities

**** [Pricing](https://cursor.com/en/pricing) | [GPT-5.1-Codex-Max Announcement](https://forum.cursor.com/t/gpt-5-1-codex-max-available-in-cursor/145277)

---

### [OpenAI Codex CLI](https://github.com/openai/codex)

> **Free with ChatGPT Plus ($20/mo):** 30–150 messages/5 hours for coding tasks
- **ChatGPT Pro ($200/mo):** 300–1,500 messages/5 hours — highest usage limits
- **Pay-as-you-go API:** GPT-5.1-Codex-Max at $1.25/$10 per million tokens (input/output)
- **Free OSS mode:** Access to open-source models only (via --oss flag)
- **GPT-5.1-Codex-Max** (Nov 19, 2025): 77.9% SWE-bench Verified — now default model
- First model with "compaction" for multi-million token sessions (24+ hour tasks)
- 30% fewer thinking tokens than previous GPT-5.1-Codex
- Also available in GitHub Copilot (Pro, Pro+, Business, Enterprise)
- Windows support now included
- Cross-platform: macOS 12+, Ubuntu 20.04+, Windows 11 via WSL2

**** [GitHub Repo](https://github.com/openai/codex) | [GPT-5.1-Codex-Max Announcement](https://openai.com/index/gpt-5-1-codex-max/)

---

### [Codeium](https://codeium.com/)

> **Pro ($10/mo):** Unlimited usage with advanced context awareness
- Claude 3.5 Sonnet, GPT-4o access
- Enhanced context window and personalization
- **Teams ($12/user/mo):** Pro features + team management
- **Enterprise (Custom):** On-premise deployment, custom models

**** [Pricing](https://codeium.com/pricing)

---

### [Tabnine](https://www.tabnine.com/)

> **Pro ($12/mo):** Enhanced AI completions and chat
- **Enterprise ($39/user/mo):** Multiple LLMs, private deployment
- Models: Claude 3.5 Sonnet, GPT-4o, Llama 3.3 70B, proprietary models
- 600+ programming languages supported
- On-premises and air-gapped deployment options
- Bring your own fine-tuned models

**** [Pricing](https://www.tabnine.com/pricing/)

---

### [JetBrains AI Assistant](https://www.jetbrains.com/ai/)

> **AI Pro ($15/mo):** Increased cloud quota + unlimited local models
- **AI Ultimate ($25/mo):** Maximum cloud quota + advanced features
- Free tier: Unlimited code completion + local models + limited cloud quota
- 30-day Pro trial included
- All Products Pack includes AI Pro
- Offline mode with local models via Ollama/LM Studio

**** [AI Pricing](https://www.jetbrains.com/ai-ides/buy/)

---

### [Jules](https://jules.google/)

> **Pro ($19.99/mo via Google AI Pro):** 100 tasks/day
- 5x higher limits than free tier (15 tasks/day → 100 tasks/day)
- 5x concurrent tasks (3 → 15 concurrent)
- Higher access to latest models
- **Ultra (via Google AI Ultra):** 300 tasks/day
- 20x higher limits than free tier
- 60 concurrent tasks
- Priority access to latest models
- Gmail account required (18+ years)

**** [Usage Limits](https://jules.google/docs/usage-limits/) | [Google AI Plans](https://one.google.com/about/google-ai-plans/)

---

### [SuperMaven](https://supermaven.com/)

> **Pro ($10/mo):** 1M token context window + chat credits
- Alternative: $99/year
- Chat interface with GPT-4o, Claude 3.5 Sonnet, GPT-4
- **Team ($10/user/mo):** Pro features + team management
- Note: Merged with Cursor IDE in November 2024

**** [Pricing](https://supermaven.com/pricing)

Know better pricing or limits? Share a link in an issue or PR to help keep this updated. See CONTRIBUTING.md for guidelines.

---

## 4. Tools with Free Access to Basic Models
__(unspecified/basic models)__

### [Bolt.new](https://bolt.new/)

> **Unspecified models**
- 1M tokens/month limit
- Specific model not publicly specified
- Credit card required

**** [Token Documentation](https://support.bolt.new/account-and-subscription/tokens)

---

### [Lovable](https://lovable.dev/)

> **Unspecified models**
- 5 daily credits, max 30 per month (free)
- Models not publicly enumerated
- Credit card required

**** [Messaging Limits](https://docs.lovable.dev/user-guides/messaging-limits)

---

### [v0.dev](https://v0.dev/)

> **Proprietary models (not frontier)**
- GPT-5 access requires v0 Premium subscription
- $5 in credits/month limit
- Uses proprietary models with varied routing
- Credit card required

**** [Updated Pricing Blog](https://vercel.com/blog/improved-v0-pricing-5luSrdRUJsRvf1kXWoYGxh)

---

### [Codeium](https://codeium.com/)

> **Unlimited free usage of basic AI coding assistance**
- Individual plan: Free forever with unlimited code completions, AI chat, commands
- 70+ programming languages supported
- IDE integrations: VS Code, JetBrains, Vim/Neovim, Jupyter
- No credit card required
- Limited context awareness (expanded in paid tiers)
- Base model only (Llama 3.1 70B), pro-graded models require subscription

**** [Pricing](https://codeium.com/pricing) | [Documentation](https://codeium.com/docs)

---

### [Tabnine](https://www.tabnine.com/)

> **Free tier with limited features**
- Basic AI code completions and chat (limited)
- Local processing available
- Context heavily limited in free tier
- Performance dialed down to save resources
- 600+ programming languages supported

**** [Pricing](https://www.tabnine.com/pricing/)

---

### [JetBrains AI Assistant](https://www.jetbrains.com/ai/)

> **AI Free tier included with IDEs**
- Unlimited code completion and local model support
- Limited quota for cloud-based features
- 30-day AI Pro trial
- Chat, code generation, commit messages with local models

**** [AI Features](https://www.jetbrains.com/ai-assistant/)

---

### [SuperMaven](https://supermaven.com/)

> **Free tier with basic features**
- Basic code suggestions
- 7-day data retention limit
- Credit card required for registration
- 1M token context window (impressive for free tier)

**** [Pricing](https://supermaven.com/pricing)

---

### [Continue.dev](https://www.continue.dev/)

> **Free open-source extension with flexible model support**
- Free VS Code and JetBrains extension
- Full support for local models via Ollama, LM Studio
- Solo tier: Private/team/public visibility options
- Supports 200+ models (requires your own API keys for cloud models)
- Community hub for custom AI assistants
- No vendor lock-in or usage limits for local models

**** [GitHub](https://github.com/continuedev/continue) | [Model Hub](https://hub.continue.dev/explore/models)

Know the official limits or models? Share a link in an issue or PR to update the information. See CONTRIBUTING.md for guidelines.

---

## 5. Local Models


Running open-weight frontier models locally provides unlimited coding assistance without API costs or usage limits. Popular tools for local deployment include **[Cline](https://cline.bot/)** (VS Code extension), **[Continue.dev](https://www.continue.dev/)**, and **[Cursor](https://cursor.com/)** (with local mode).

**Recommended Models by Size**:

| Model | Size | Type | Speed | Quality |
|-------|------|------|-------|---------|
| Qwen2.5-Coder-32B | 20GB | Balanced | ⚡⚡⚡ | ⭐⭐⭐⭐⭐ |
| Mistral-7B | 4GB | Lightweight | ⚡⚡⚡⚡⚡ | ⭐⭐⭐ |
| Deepseek-v3 | 150GB | Heavyweight | ⚡ | ⭐⭐⭐⭐⭐ |
| Llama-70B | 40GB | Heavy | ⚡⚡ | ⭐⭐⭐⭐ |

**Quick Setup**:
```bash
brew install ollama
ollama pull qwen2.5-coder:32b
# Start server: ollama serve
# In VS Code Continue.dev:
# Set provider to ollama, model to qwen2.5-coder:32b
```

**Note**: Frontier models require substantial RAM/VRAM. In particular, for Qwen3‑Coder‑480B the Ollama‑friendly GGUF is ~150GB, and practical local inference can require ~150GB of unified memory.

---

## Comparison Notes

- **Goal**: Compare AI coding tools by their access to pro-grade models and free tier limits.
- **What qualifies a model as "pro-grade"?** Models must achieve ≥60% on SWE-bench Verified, demonstrating real-world software engineering capability. Current qualifying models: Claude Opus 4.5, GPT-5.1-Codex-Max, Claude Sonnet 4.5, Gemini 3 Pro, and others listed above.
- **Different limit types**: Tools use various quota systems - requests, tokens, credits, chats - making direct comparison challenging. Check documentation for specifics.
- **Real-world usage**: Actual consumption varies dramatically based on coding style, task complexity, and tool implementation.
- **Stacking strategy**: Combining multiple free tiers can effectively triple or quadruple your capacity with zero cost.

---

## Related Resources

- [Coding with AI](https://coding-with-ai.dev/) - Practical techniques and resources for coding with LLMs
- [Free LLM API Resources](https://github.com/cheahjs/free-llm-api-resources) - Comprehensive list of free LLM APIs for building custom integrations
- [Ollama Models Library](https://ollama.ai/library) - Browse and download open-source models for local use

---
