---
title: "Frequently Asked Questions (FAQ)"
description: "Common questions and answers about using OpenCode"
---

# Frequently Asked Questions (FAQ)

## 📝 Course Notes
Key takeaways from this lesson:

<img src="/images/appendix/faq-notes.mini.jpeg"
     alt="FAQ Course Notes"
     data-zoom-src="/images/appendix/faq-notes.jpeg" />

> Having issues? Check here first

---

## Installation Issues

### Q: Install command returns "command not found"

**A**: Your PATH environment variable may not be set correctly.

```bash
# Check installation location
which opencode

# If no output, manually add to PATH
# macOS/Linux
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Or use npm global install
npm install -g @anthropic-ai/opencode
```

---

### Q: Installation fails on Windows

**A**: We recommend using a package manager:

```powershell
# Using Scoop
scoop install opencode

# Or using Chocolatey
choco install opencode

# Or using npm
npm install -g @anthropic-ai/opencode
```

Make sure to run the terminal as Administrator.

---

### Q: macOS shows "cannot verify developer"

**A**: This is a macOS security restriction.

```bash
# Method 1: Right-click the app and select "Open"
# Method 2: Run in terminal
xattr -d com.apple.quarantine /path/to/opencode
```

---

### Q: Features break after version update

**A**: Try clearing the cache and reinstalling:

```bash
# Clear cache
rm -rf ~/.cache/opencode

# Reinstall
opencode upgrade --force
```

---

## Network Issues

### Q: Connection timeout with "ETIMEDOUT" or "ECONNREFUSED"

**A**: This is a network connectivity issue.

**Solution 1: Set up proxy**
```bash
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
opencode
```

**Solution 2: Use alternative providers**
```bash
# Switch to providers with better regional access
opencode
/connect  # Select your preferred provider
```

See [Network Configuration](../1-start/03-network).

---

### Q: Proxy is set but still cannot connect

**A**: Check the following:

1. Confirm proxy software is running
2. Verify proxy port is correct
3. Check if NO_PROXY needs to be set
4. Test with `curl`:

```bash
curl -x http://127.0.0.1:7890 https://api.anthropic.com
```

---

### Q: How to handle corporate network certificates

**A**: Set custom certificates:

```bash
export NODE_EXTRA_CA_CERTS=/path/to/certificate.pem
opencode
```

Or configure in the config file:

```json
{
  "network": {
    "ca_cert": "/path/to/certificate.pem"
  }
}
```

---

### Q: API blocked by corporate firewall

**A**: Corporate firewalls often block API endpoints. Try these solutions:

1. **Use a corporate-approved VPN** if available
2. **Self-hosted models**: Deploy local models like Ollama
   ```bash
   # Install Ollama
   curl -fsSL https://ollama.com/install.sh | sh
   
   # Run a model
   ollama run codellama
   
   # Configure OpenCode to use local model
   opencode
   /connect  # Select Ollama
   ```
3. **Request firewall exception** from IT for specific API domains
4. **Use proxy with authentication**:
   ```bash
   export HTTPS_PROXY=http://corporate-proxy:8080
   export NO_PROXY=localhost,127.0.0.1,internal.company.com
   ```

---

## International User Issues

### Q: API access from restricted regions

**A**: Some regions have limited access to certain AI providers:

1. **Use alternative providers** available in your region:
   - Europe: Mistral, DeepSeek
   - Asia: Z.AI (Zhipu), DeepSeek, Moonshot
   - Global: OpenAI, Anthropic (may require VPN)

2. **Configure regional endpoints** if available:
   ```json
   {
     "provider": {
       "anthropic": {
         "options": {
           "baseURL": "https://your-regional-endpoint.com"
         }
       }
     }
   }
   ```

3. **Use local models** for complete offline access

---

### Q: International payment issues for API credits

**A**: Many AI providers accept international payments, but options vary:

| Provider | Payment Methods | Regional Notes |
|----------|-----------------|----------------|
| OpenAI | Credit/Debit cards, PayPal | Most regions supported |
| Anthropic | Credit/Debit cards | US/UK/EU preferred |
| DeepSeek | Alipay, WeChat Pay, cards | Good for Asia |
| Mistral | Credit cards | EU-focused |
| Z.AI | Alipay, cards | China-focused |

**Tips:**
- Use virtual cards (like Revolut, Wise) for international payments
- Check if provider offers prepaid credits
- Consider third-party API aggregators (OpenRouter, Together AI)

---

### Q: Latency issues from different regions

**A**: Optimize for your region:

1. **Choose nearby regions**:
   ```json
   {
     "provider": {
       "openai": {
         "options": {
           "baseURL": "https://api.openai.com/v1"  // or regional endpoint
         }
       }
     }
   }
   ```

2. **Use smaller models** for faster response
3. **Enable streaming** for perceived performance:
   ```json
   {
     "stream": true
   }
   ```
4. **Consider local models** for zero latency

---

### Q: Data residency and compliance requirements

**A**: For organizations with data residency requirements:

1. **Check provider data centers**:
   - AWS Bedrock: Multiple regions (us-east, eu-west, ap-northeast)
   - Azure OpenAI: Available in multiple Azure regions
   - Google Vertex AI: Global regions available

2. **Use self-hosted models** for complete data control
3. **Review provider compliance** (SOC2, GDPR, HIPAA)
4. **Configure data processing agreements** with your provider

---

## Model Configuration Issues
<AdInArticle />

### Q: API Key is set but getting "authentication failed"

**A**: Check the following:

1. **API Key format is correct**: Different providers have different formats
   - Anthropic: `sk-ant-xxx`
   - OpenAI: `sk-xxx`
   - DeepSeek: `sk-xxx`

2. **API Key is valid**: Test on the provider's website

3. **Environment variable is set correctly**:
   ```bash
   echo $ANTHROPIC_API_KEY  # Check if it has a value
   ```

4. **Config file syntax is correct**:
   ```bash
   cat ~/.config/opencode/opencode.json | jq .  # Check JSON format
   ```

---

### Q: Getting "model unavailable" or "quota exceeded"

**A**: 

1. **Quota exhausted**: Check your provider account balance
2. **Wrong model name**: Verify the model identifier is correct
3. **Account restrictions**: Some models require paid accounts

```bash
# List available models
opencode models
```

---

### Q: How to switch between different models

**A**: 

**Method 1: Switch in TUI**
```
/models
```

**Method 2: Specify via command line**
```bash
opencode -m deepseek-chat
```

**Method 3: Set default in config file**
```json
{
  "model": "deepseek-chat"
}
```

---

### Q: How to configure multiple providers

**A**: Add multiple providers in the config file:

```json
{
  "provider": {
    "anthropic": {
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}"
      }
    },
    "deepseek": {
      "options": {
        "apiKey": "{env:DEEPSEEK_API_KEY}"
      }
    },
    "openai": {
      "options": {
        "apiKey": "{env:OPENAI_API_KEY}"
      }
    }
  }
}
```

Then switch with `/models`.

---

## Permission Issues

### Q: Confirming every action is annoying

**A**: You can set permission modes:

**Method 1: Auto-allow for this session**
- Press `a` key to select "always allow"

**Method 2: Set in config file**
```json
{
  "permission": {
    "read": "allow",
    "edit": "allow",
    "bash": "allow"
  }
}
```

**Method 3: Fine-grained control**
```json
{
  "permission": {
    "read": "allow",
    "edit": "ask",
    "bash": "ask"
  }
}
```

---

### Q: AI executed a command I didn't want

**A**: 

1. Press `Ctrl+C` to interrupt immediately
2. Use `/undo` to revert file changes
3. Set stricter permissions:

```json
{
  "permission": {
    "bash": "ask"
  }
}
```

---

### Q: How to restrict AI to read-only mode

**A**: Use Plan mode:

1. Press `Tab` to switch to Plan mode
2. Or specify Agent at startup:
   ```bash
   opencode -a plan
   ```

---

## Performance Issues

### Q: Response is very slow

**A**: Possible causes and solutions:

1. **Network latency**: Use proxy or switch to local models
2. **Model too large**: Use smaller models (like `small_model`)
3. **Context too long**: Use `/compact` to compress context

---

### Q: Context too long causing errors

**A**: 

```bash
# Manual compression
/compact

# Compression options in config
{
  "compaction": {
    "auto": true,
    "prune": true
  }
}
```

> `auto`: Automatically compress when context is full; `prune`: Remove old tool outputs to save tokens

---

### Q: High memory usage

**A**: 

1. Close unused sessions
2. Configure file watcher to ignore directories:
   ```json
   {
     "watcher": {
       "ignore": ["node_modules/**", "dist/**", ".git/**"]
     }
   }
   ```
3. Use smaller models

---

## Feature Issues

### Q: How to make AI remember my preferences

**A**: Use AGENTS.md or CLAUDE.md files:

```markdown
<!-- AGENTS.md -->
# Project Rules

- Use TypeScript
- Use pnpm instead of npm
- Code comments in English
- Follow ESLint rules
```

Or run `/init` to auto-generate.

---

### Q: Can't find previous sessions

**A**: 

```bash
# List all sessions
opencode session list

# View in TUI
/sessions
```

Sessions are stored in `~/.local/share/opencode/sessions/`.

---

### Q: How to export conversation history

**A**: 

```bash
# Export in TUI
/export

# Export via command line
opencode session export <session-id> -o conversation.md
```

---

### Q: File changes not taking effect

**A**: Check the following:

1. Confirm you're in Build mode (not Plan mode)
2. Check file permissions
3. See if permission prompts were ignored
4. Use `/details` to view operation details

---

### Q: Git undo/redo not working

**A**: 

1. Confirm project is a Git repository
2. Confirm there are uncommitted changes
3. Check Git status:
   ```bash
   git status
   ```

---

## Compatibility Issues

### Q: Terminal shows garbled characters

**A**: 

1. Use recommended terminals: WezTerm / Alacritty / iTerm2
2. Set correct encoding:
   ```bash
   export LANG=en_US.UTF-8
   ```
3. Use supported fonts (Nerd Fonts recommended)

---

### Q: Keyboard shortcuts not working

**A**: 

1. Check if terminal intercepts shortcuts
2. Some terminals need special configuration
3. Try using slash commands instead

---

### Q: Can't find VS Code extension

**A**: 

```bash
# Manually install extension
code --install-extension anthropic.opencode

# Or search "OpenCode" in VS Code
```

---

## Other Issues

### Q: How to get help

**A**: 

1. View help: `/help`
2. View docs: [opencode.ai/docs](https://opencode.ai/docs)
3. Submit Issue: [github.com/vbgate/learn-opencode](https://github.com/vbgate/learn-opencode)

---

### Q: How to report bugs

**A**: 

1. Collect information:
   ```bash
   opencode --version
   uname -a
   echo $SHELL
   ```

2. Steps to reproduce

3. Submit Issue on GitHub

---

### Q: How to contribute code

**A**: 

1. Fork the repository
2. Create a branch
3. Submit a PR
4. Wait for review

See [Contributing Guide](https://github.com/anomalyco/opencode/blob/dev/CONTRIBUTING.md)

---

## Related Resources

- [Troubleshooting](./troubleshoot) - Detailed troubleshooting
- [Network Configuration](../1-start/03-network) - Network issue solutions
- [Model Providers](./providers) - Available model list

::: tip Can't find your answer?
[Join the community](/en/community) to connect with 2000+ fellow learners and get real-time support.
:::
