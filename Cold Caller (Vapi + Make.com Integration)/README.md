# AI Cold Caller Template | Vapi + Make.com

> Complete automation template for building dynamic, scalable AI voice assistants for outbound calling campaigns.

## What It Does

Transforms static Vapi assistants into **dynamic, data-driven AI callers** that personalize every conversation using real-time lead data from Google Sheets.

### Key Features

- **Dynamic Variable Injection** - Use custom tags `[first_name]`, `[country]`, `[current_time]`, `[job_title]` etc. in prompts
- **Round-Robin Phone Numbers** - Automatically cycles through multiple phone numbers to avoid rate limits and maintain caller ID reputation
- **Automated Lead Management** - Tracks call status (called/not-called) and updates Google Sheets in real-time
- **Complete Call Transcripts** - Stores full conversation transcripts with metadata for every call
- **Built-in Reporting Dashboard** - Visual analytics showing total leads, call completion rates, and call end reasons
- **Scalable Architecture** - Handles 1,000+ leads per batch with customizable throttling
- **No-Code Setup** - Built entirely with Make.com workflows and Google Sheets

## Requirements

| Tool | Purpose |
|------|---------|
| [Vapi](https://vapi.ai) | AI voice assistant platform |
| [Make.com](https://make.com) | Workflow automation (2 scenarios) |
| [Google Sheets](https://sheets.google.com/) | Lead database & reporting |
| JSON Editor Online | Optional: For adding custom dynamic variables |

## Use Cases

### Sales & Outreach
- **Cold calling** prospects with personalized pitches
- **Lead qualification** and appointment setting
- **Product demo scheduling** with context-aware conversations

### Customer Service
- **Proactive outreach** to customers with account updates
- **Survey calls** with dynamic questionnaires
- **Renewal reminders** with personalized offers

### Operations
- **Appointment confirmations** with rescheduling options
- **Payment reminders** with account-specific details
- **Status update calls** for orders/services

### Scalability Features
- Multi-number rotation prevents carrier flagging
- Batch processing for high-volume campaigns
- Real-time status tracking prevents duplicate calls

## How It Works

```
Lead Database (Google Sheets)
        ↓
Make.com Scenario #1 (Main Workflow)
        ↓
Vapi Assistant (Dynamic + Transient)
        ↓
Make.com Scenario #2 (Callbacks)
        ↓
Updated Transcripts + Reports
```

1. **Leads** stored in Google Sheets with status tracking
2. **Make.com workflow** fetches uncalled leads every 15 minutes
3. **Dynamic variables** replace tags in assistant prompts
4. **Vapi makes calls** using round-robin phone numbers
5. **Callbacks** capture transcripts and update lead status
6. **Dashboard** shows real-time analytics

## Quick Start

1. Copy the [Google Sheet template](https://docs.google.com/spreadsheets/d/14wzCqpwIdh-fshCmMGEvX8Y-RlZop9ITa4AwAHiDgHU/edit?usp=sharing)
2. Import blueprints into Make.com:
   - `ai-cold-caller-template-2-0.json` (Main workflow)
   - `ai-cold-caller-template-2-0-callbacks.json` (Webhook handler)
3. Connect Google Sheets & Vapi API
4. Add phone numbers to Phone Number Reference tab
5. Upload leads to Leads tab
6. Activate scenarios

## Template Files

- `ai-cold-caller-template-2-0.json` - Main calling workflow
- `ai-cold-caller-template-2-0-callbacks.json` - Callback webhook handler
- [Google Sheet Template](https://docs.google.com/spreadsheets/d/14wzCqpwIdh-fshCmMGEvX8Y-RlZop9ITa4AwAHiDgHU/edit?usp=sharing)
