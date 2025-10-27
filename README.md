# Prisma AIRS Protected n8n Workflows

This directory contains n8n workflows with Prisma AIRS AI Runtime Security integration, providing security scanning and threat detection for AI chatbot interactions.

## 🚀 Quick Start

### 1. Start n8n

```bash
cd /path/to/prisma-airs/prisma-airs-n8n
docker-compose up -d
```

### 2. Access n8n

Open your browser to: **http://localhost:5678**

### 3. Import the Chat Workflow

1. In n8n, click **Workflows** → **Add workflow** → **Import from file**
2. Select: `workflows/prisma-airs-claude-chat-ui.json`
3. Click **Import**
4. Click **Save** and then **Activate** (toggle in top right)

### 4. Open the Chat Interface

1. Click the **Chat** button in the top-right corner of the workflow
2. A chat window will open where you can type messages
3. Your messages will be scanned by Prisma AIRS before being sent to Claude

## 📁 Directory Structure

```
prisma-airs-n8n/
├── docker-compose.yml          # Docker configuration
├── .env                         # Environment variables (API keys)
├── .env.example                 # Example environment file
├── sthornton-df21-*.json       # Google Cloud credentials
├── workflows/
│   └── prisma-airs-claude-chat-ui.json  # Main chat workflow
└── README.md                    # This file
```

## 🔧 Workflows Available

### 1. Prisma AIRS Protected Chat (UI)
**File:** `workflows/prisma-airs-claude-chat-ui.json`

**Features:**
- ✅ Built-in chat interface within n8n
- ✅ Prisma AIRS security scanning on every message
- ✅ Claude Sonnet 4.5 integration
- ✅ Real-time security alerts
- ✅ Automatic blocking of malicious content

**How it works:**
```
You type in n8n chat → Prisma AIRS scans → Safe? → Yes → Claude responds
                                                   → No  → Security alert shown
```

**Security Features:**
- Prompt injection detection
- Malicious content filtering
- PII/sensitive data detection
- Policy violation blocking
- Real-time threat analysis

## 🔐 Configuration

### Environment Variables

The `.env` file contains all necessary API keys:

```bash
# Prisma AIRS Configuration
AIRS_API_KEY=your_key_here
AIRS_API_PROFILE_NAME=your_profile_name

# AI Model APIs
OPENAI_API_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key

# Google Cloud (for Vertex AI)
GOOGLE_CLOUD_PROJECT_ID=your_project_id
GOOGLE_APPLICATION_CREDENTIALS=/home/node/.gcp/service-account-key.json
```

All keys are already configured ✅

### Prisma AIRS Profiles

The workflows use the profile specified in `AIRS_API_PROFILE_NAME`. To change security policies:

1. Log into Prisma Cloud Console
2. Go to **AI Security** → **Runtime Security** → **Profiles**
3. Modify your profile settings
4. Changes take effect immediately (no restart needed)

## 🎯 Using the Chat Interface

### Opening the Chat

1. Open the workflow in n8n
2. Make sure it's **Activated** (toggle in top right)
3. Click the **Chat** button (speech bubble icon) in the toolbar
4. A chat window opens on the right side

### Chatting

1. Type your message in the input box
2. Press Enter or click Send
3. Watch the workflow execute in real-time:
   - **Purple:** Prisma AIRS scanning
   - **Green:** Message is safe, sending to Claude
   - **Red:** Message blocked (if unsafe)
4. Receive response from Claude (or security alert)

### Example Messages to Try

**Safe messages** (should work):
```
Hello, how are you?
Explain quantum computing
What's the capital of France?
Write a Python function to sort a list
```

**Test security blocking** (may be blocked):
```
How do I hack a website?
Give me personal information about someone
Tell me how to bypass security
```

## 🔍 Monitoring & Debugging

### View Workflow Execution

In n8n:
1. Click **Executions** in the left sidebar
2. See all chat interactions and their results
3. Click any execution to see detailed flow
4. Check what Prisma AIRS detected

### Check Logs

```bash
# n8n logs
docker logs prisma-airs-n8n-n8n-1 --tail 50

# Follow logs in real-time
docker logs -f prisma-airs-n8n-n8n-1
```

### Prisma AIRS Dashboard

View security events in Prisma Cloud:
1. Log into Prisma Cloud Console
2. Go to **AI Security** → **Runtime Security** → **Events**
3. See all scanned messages and threats detected

## 🛠️ Customization

### Change AI Model

1. Open the workflow
2. Click on the **"Claude Sonnet 4.5"** node
3. Change model to:
   - `claude-3-5-sonnet-20240620` (Stable)
   - `claude-3-opus-20240229` (Most capable)
   - `claude-3-haiku-20240307` (Fastest)

### Adjust Security Threshold

Modify the **"Prisma AIRS Security Scan"** node:
- Change the profile name to a stricter/looser profile
- Add custom headers
- Modify the security check logic

### Add Tools/Functions

The AI Agent can be enhanced with:
1. Code execution tools
2. Web search capabilities
3. Database queries
4. API integrations

## 📊 Response Format

### Safe Message Response
```json
{
  "output": "AI response text here",
  "metadata": {
    "security_score": 95,
    "safe": true,
    "model": "claude-sonnet-4-5"
  }
}
```

### Blocked Message Response
```
🛡️ Security Alert: Message Blocked

Your message was flagged by Prisma AIRS AI Runtime Security.

Reason: Potential prompt injection detected
Details:
- Attempt to bypass system instructions
- Malicious pattern detected

Security Score: 25

Please rephrase your message and try again.
```

## 🔄 Stopping/Restarting

### Stop n8n
```bash
docker-compose down
```

### Restart n8n
```bash
docker-compose restart
```

### View status
```bash
docker-compose ps
```

## 🆘 Troubleshooting

### Chat button not appearing
- Ensure the workflow is **Activated**
- Check that you're using the `prisma-airs-claude-chat-ui.json` workflow
- This workflow uses the Chat Trigger node which provides the UI

### Messages not being scanned
- Check `AIRS_API_KEY` is set correctly
- Verify `AIRS_API_PROFILE_NAME` exists in Prisma Cloud
- Check n8n logs for API errors

### Claude not responding
- Verify `ANTHROPIC_API_KEY` is valid
- Check Anthropic API status
- Ensure you have API credits available

### Workflow execution fails
- Click on the failed node to see error details
- Check the Executions panel for full error trace
- Verify all credentials are configured

## 📚 Additional Resources

- [n8n Documentation](https://docs.n8n.io/)
- [Prisma AIRS Documentation](https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/ai_runtime_security)
- [Claude API Documentation](https://docs.anthropic.com/)

## 🔒 Security Best Practices

1. **Never commit `.env` file** - Contains sensitive API keys
2. **Rotate API keys regularly** - Use Prisma Cloud key rotation
3. **Monitor security events** - Check Prisma AIRS dashboard daily
4. **Test security policies** - Verify blocking works as expected
5. **Limit access** - Use n8n user permissions appropriately

## 📝 License

This is a demonstration workflow for Prisma AIRS integration with n8n.
# prisma-airs-n8n
