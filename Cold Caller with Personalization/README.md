# 🤖📞 AI Cold Caller with Dynamic Personalization

> Transform Vapi's static assistants into dynamic, data-driven calling machines with real-time personalization from Google Sheets.

---

## 🎯 What It Does

This n8n/Make.com automation converts static Vapi assistants into **transient-based assistants** with dynamic data injection. Each call is personalized using real-time lead data, automatic phone number rotation, and comprehensive tracking.

**Core Capabilities:**
- 🎭 **Dynamic Personalization** - Inject lead data (name, location, job title, etc.) into conversations via custom tags
- 🔄 **Smart Phone Number Rotation** - Round-robin through multiple numbers to avoid rate limits and maintain caller ID reputation
- 📊 **Automatic Call Logging** - Transcripts, outcomes, and performance metrics auto-saved to Google Sheets
- 🚀 **Scalable Architecture** - Handle 1 to 1,000+ calls without configuration changes
- 🎯 **Tag-Based System** - Use `[first_name]`, `[current_time]`, `[job_title]` etc. in prompts - automatically replaced per call
- 📈 **Live Reporting Dashboard** - Real-time metrics on call status, end reasons, and phone number performance

**The Technical Difference:**
Vapi's default = Static assistant with fixed prompts
This automation = Transient assistants generated per-call with dynamic data insertion

---

## 💼 Use Cases

| Industry | Application |
|----------|-------------|
| 🏠 Real Estate | Property outreach with address-specific details |
| 💊 Healthcare | Patient follow-ups with personalized health info |
| 🛍️ E-commerce | Abandoned cart recovery with product details |
| 🎓 Lead Qualification | Inbound lead calls with inquiry context |
| 📅 Events | RSVP confirmations with event-specific data |
| 💰 Collections | Payment reminders with account information |
| 🔔 Retention | Win-back campaigns with customer history |

---

## 📦 Output Types

### 1. Real-Time Reporting Dashboard (Google Sheets)
- Total leads counter
- Called vs Not-Called breakdown
- End-call reason distribution charts
- Phone number performance metrics
- Dynamic status updates

### 2. Call Transcripts & Metadata
Each call generates:
- Full conversation transcript
- Phone number used (ID from pool)
- Call outcome/end reason
- Lead data snapshot
- Timestamp & duration

### 3. Lead Status Management
- Auto-updates: Not-Called → Called
- Phone number assignment tracking
- Duplicate call prevention
- Status change logging

### 4. Phone Number Pool Management
- Round-robin distribution
- Active/Inactive status tracking
- Automatic flagged number exclusion
- Load balancing across numbers

---

## 🛠️ Requirements

| Tool | Purpose | Cost |
|------|---------|------|
| [Vapi](https://vapi.ai) | AI voice calling engine | ~$0.05-0.10/min (pay-as-go) |
| [Make.com](https://make.com) | Workflow automation | Free tier: 1K ops/month |
| [Google Sheets](https://sheets.google.com/) | Lead database & reporting | Free |
| [JSONaut](https://jsonaut.com/) | JSON editing (optional) | Free |

**Total startup cost:** $0 (free tiers available for all tools)

---

## ⚡ Installation

### 1. Get Templates
- Download `Dynamic-Cold-Caller-Vapi.json` (main workflow)
- Download `Dynamic-Cold-Caller-Sync-Data.json` (callbacks)
- Copy [Google Sheet Template](https://docs.google.com/spreadsheets/d/1FrH27nX0v56311WS5917MnXF_ox0ZXcKn5jLyDGC0gA/edit?usp=sharing)

⚠️ **Don't rename sheet tabs** - automation expects specific names

### 2. Import to Make.com
```
Make.com → New Scenario → "..." → Import Blueprint
→ Upload JSON files → Connect Google Sheets → Select spreadsheet
```

### 3. Configure Vapi
```
1. Create static assistant in Vapi
2. Copy Assistant ID → Paste in Make scenario
3. Add Vapi API key to scenario
4. Vapi → Advanced → Server URL → Add Make webhook URL
```

### 4. Setup Phone Numbers
```
Vapi → Phone Numbers → Copy IDs
Google Sheet "Phone Numbers" tab → Paste IDs → Set status: "Active"
```

### 5. Add Leads & Launch
```
Google Sheet "Lead List" tab → Add leads
Make.com → Click "Run Once"
```

---

## 🎨 Customization

### Adding Custom Tags

**Example:** Add `[job_title]` tag

1. **Google Sheet:** Add "Job Title" column
2. **Make.com:** Edit "Dynamic Variables" module
3. **JSON Editor:** Add new tag using [JSONaut](https://jsonaut.com/)
```json
{
  "user_job_title": "{{column_value}}"
}
```
4. **Map Column:** Link Google Sheet column to tag
5. **Use in Prompts:** `[job_title]` now available

### Example Prompts

**First Message:**
```
Hi [first_name], this is Sarah calling from Bright Horizons Realty,
how are you doing today?
```

**System Prompt:**
```
# AI Cold Call Agent for Bright Horizons Realty

**Objective:** Engage with cold-called users to inquire about their
interest in selling their property, using a friendly and concise approach.

The current time is [current_time]

**Details about the user:**
- First name: [first_name]
- Location: [user_country]
- Job Title: [job_title]

**Instructions for AI Agent:**
1. Introduction: Begin by introducing yourself and the company.
2. Purpose of Call: State the purpose early on.
3. Use of Fillers: Use "uhm", "ah", "gotcha" for natural conversation.
4. Engage the User: Refocus if user seems distracted.
5. Information Gathering: Collect property details if interested.
6. Closure: Thank user and outline next steps.
7. Friendly Tone: Maintain positive demeanor throughout.
```

---

## 📊 Google Sheet Structure

| Tab | Purpose |
|-----|---------|
| **Reporting** | Live dashboard with charts & metrics |
| **Lead List** | Your leads with status tracking |
| **Transcripts** | Auto-logged call records |
| **Phone Numbers** | Phone number pool management |

---

## 🔗 Resources

- 🎙️ [Vapi Platform](https://integraticus.com/share/vapi/)
- ⚙️ [Make.com Automation](https://make.com/)
- 🔧 [JSONaut Editor](https://jsonaut.com/)
- 📊 [Google Sheet Template](https://docs.google.com/spreadsheets/d/1FrH27nX0v56311WS5917MnXF_ox0ZXcKn5jLyDGC0gA/edit?usp=sharing)

---

## ✅ Why Use This

| Benefit | Description |
|---------|-------------|
| 🎯 **Beginner-Friendly** | No coding required (JSON customizable) |
| 💰 **Cost-Effective** | Cheaper than Bland AI, Synthflow alternatives |
| 🔓 **Full Control** | Own your data, customize everything |
| 📈 **Scalable** | 10 calls to 10K+ with same setup |
| 👁️ **Transparent** | Every call logged with full transcript |
| 🔧 **Flexible** | Works across any industry/use case |

---

## 🚀 Technical Highlights

- **Tag System:** Bracket notation `[tag_name]` auto-replaced with lead data
- **Round-Robin Logic:** Prevents rate limits via phone number cycling
- **Transient Assistants:** Generated per-call, not stored in Vapi
- **Webhook-Driven:** Real-time callbacks for logging and status updates
- **Error Handling:** Inactive number detection, duplicate call prevention
- **Data Validation:** Status checks before call initiation

---

**Built for scalability. Designed for personalization. Optimized for results.** 🎯

---

*Transform your static AI into a dynamic calling powerhouse. Your leads deserve better than robotic outreach.* 📞✨
