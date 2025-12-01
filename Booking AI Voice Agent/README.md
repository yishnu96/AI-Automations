# 🤖 AI Voice Booking Agent

Automated appointment booking system using AI voice agent that handles scheduling, availability checking, and notifications without human intervention.

## 📖 Overview

An intelligent voice agent that automates phone-based appointment booking using **VAPI** (voice AI), **N8N** (workflow automation), and **Cal.com** (calendar management). The system uses defined logic for reliability while maintaining natural conversation flow.

**Watch Tutorial**: [YouTube - AI Voice Booking Agent](https://www.youtube.com/watch?v=b09o75A-X2E&t=2713s)

## ✨ What It Does

- **Natural Conversations** - AI agent talks to callers using ElevenLabs voice
- **Checks Availability** - Queries Cal.com calendar in real-time
- **Books Appointments** - Creates calendar events automatically
- **Sends Confirmations** - SMS via Twilio with booking details
- **Logs Data** - Records all interactions in Airtable
- **Notifies Team** - Sends Slack alerts for new bookings

## 🏗️ Architecture

```
Caller → VAPI Agent → N8N Workflow → Cal.com / Twilio / Slack / Airtable
```

**Components:**
- **VAPI**: Voice agent (ElevenLabs + GPT-4o-mini + Deepgram)
- **N8N**: Automation hub connecting all services
- **Cal.com**: Calendar and booking management
- **Twilio**: SMS notifications
- **Airtable**: CRM/Database
- **Slack**: Team notifications (optional)

## 📊 Output Types

| Output | Description | Example |
|--------|-------------|---------|
| **Voice Response** | Natural AI conversation | "Your appointment is booked for Feb 15 at 2 PM" |
| **SMS** | Booking confirmation text | Date, time, meeting link, contact info |
| **Slack Alert** | Team notification | New booking with customer details |
| **Calendar Event** | Cal.com event | Auto-created with meeting link |
| **Airtable Record** | CRM data | Call transcript, booking details, customer info |

## 🎯 Use Cases

**Professional Services**: Consulting, legal, financial advising, coaching
**Healthcare**: Medical appointments, therapy, telemedicine
**Home Services**: Real estate viewings, contractor visits, inspections
**Sales & Marketing**: Demo calls, lead qualification, strategy sessions
**Education**: Tutoring, fitness training, music lessons
**24/7 Operations**: After-hours booking, high call volume handling

## 📦 Requirements

**Required Services:**
- [VAPI](https://vapi.ai) - Voice agent hosting
- [N8N](https://n8n.io) - Workflow automation
- [Cal.com](https://cal.com) - Calendar (Event Type ID + API Key)
- [Twilio](https://twilio.com) - SMS (Account SID + Auth Token + Phone number)
- [Airtable](https://airtable.com) - Database (API token)

**Optional:**
- [Slack](https://slack.com) - Team notifications
- [Postman](https://postman.com) - API configuration

## 🚀 Quick Setup

### Step 1: Create VAPI Tools (Postman)
```
POST https://api.vapi.ai/tool
```
1. Import `checkCalendarN8N` schema from `VAPI Tools (step 1).md`
2. Import `bookCalendarN8N` schema
3. Save both `toolId` values

### Step 2: Create VAPI Agent (Postman)
```
POST https://api.vapi.ai/assistant
```
1. Use schema from `VAPI AGENT (step 2).md`
2. Replace placeholders: tool IDs, N8N webhook URL
3. Adjust timezone (default: America/New_York)

### Step 3: Setup Cal.com
1. Create event type (e.g., "Discovery Call", 15 min)
2. Set availability (9 AM - 5 PM, Mon-Fri)
3. Enable "Check for conflicts"
4. Get Event Type ID (from URL) and API Key (Settings → API Keys)

### Step 4: Import N8N Workflow
1. Import `n8n.json` or `n8n-est.json`
2. Configure Cal.com nodes (API key, Event Type ID, timezone offset)
3. Activate workflow, copy webhook URL

### Step 5: Configure Airtable
1. Create 2 tables: "Raw Data" and "Bookings"
2. Generate API token: https://airtable.com/create/tokens
3. Add credentials to N8N Airtable nodes

### Step 6: Setup Twilio
1. Get Account SID + Auth Token from https://console.twilio.com/
2. Add to N8N Twilio node
3. Set "From" number to your Twilio phone

### Step 7: Connect Slack (Optional)
1. Create Slack app with permissions
2. Add credentials to N8N Slack node
3. Select notification channel

### Step 8: Test
- Make test call to VAPI agent
- Verify: Calendar event ✓ SMS sent ✓ Slack alert ✓ Airtable logged ✓

## ⚙️ Key Configuration

**Timezone Settings** (must match across all platforms):
- VAPI prompt: `{{"now" | date: "%b %d, %Y, %I:%M %p", "America/New_York"}}`
- N8N nodes: GMT offset (e.g., `-05:00` for EST)
- Cal.com event: Timezone setting

**Customization:**
- Voice: Change `voiceId` in VAPI agent schema
- Greeting: Edit `firstMessage` in agent schema
- SMS template: Modify in N8N Twilio node
- Business hours: Update in Cal.com availability + agent prompt

## 🔧 Advanced Features

From `visual-guide.md`:
- **Cancellation Management** - Handle appointment cancellations
- **User Database** - Manage customer database directly
- **Enhanced Confirmations** - Multi-channel confirmations
- **Reminders** - 24-hour and 1-hour before notifications
- **Rescheduling** - Allow customers to reschedule

## 📁 Project Files

- `VAPI Tools (step 1).md` - Tool schemas (checkCalendar, bookCalendar)
- `VAPI AGENT (step 2).md` - Agent configuration
- `N8N Guide (step 3).md` - Detailed setup instructions
- `n8n.json` / `n8n-est.json` - N8N workflow exports
- `info.md` - Project overview
- `visual-guide.md` - Advanced solutions

## 💰 Estimated Costs (~100 calls/month)

- VAPI: $50-100
- Twilio: $10-20
- Cal.com: Free-$12
- N8N: Free (self-hosted) or $20-50
- Airtable: Free-$20
- **Total: $60-200/month**

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Agent doesn't check availability | Verify N8N webhook URL in VAPI tool, check workflow is active |
| Wrong timezone | Update GMT offset in N8N, VAPI prompt, and Cal.com settings |
| SMS not sending | Check Twilio credentials, phone format (E.164), account balance |
| Double bookings | Enable "Check for conflicts" in Cal.com |

## 📚 Resources

**Platforms:**
- [VAPI Docs](https://docs.vapi.ai) | [N8N Docs](https://docs.n8n.io) | [Cal.com Docs](https://cal.com/docs)
- [Twilio Docs](https://twilio.com/docs) | [Airtable API](https://airtable.com/developers/web/api)

**Additional:**
- [Integraticus Hub](https://hub.integraticus.com) - Advanced solutions
- [Original Tutorial](https://www.youtube.com/watch?v=b09o75A-X2E&t=2713s)

## ⚠️ Important Notes

- Ensure compliance with GDPR, TCPA, and privacy regulations
- Configure HIPAA/PCI in VAPI if handling sensitive data
- Test thoroughly before production use
- Monitor costs and usage regularly

---

**Built with VAPI, N8N, Cal.com & AI**
*For educational purposes - customize for your business needs*
