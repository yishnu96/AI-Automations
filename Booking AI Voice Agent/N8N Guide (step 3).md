### **Dependencies**

1. **n8n Webhook URL**  
   * Obtain this from the imported n8n workflow.  
2. **Cal.com Event Type ID and API Key**  
   * Event Type ID is found in the event’s URL.  
   * API Key is generated under **Settings → API Keys**.  
3. **Twilio Account**  
   * Requires a phone number with SMS capability.  
4. **VAPI Account**  
   * For hosting your AI voice agent.  
5. **Airtable Base \+ Tables**  
   * Two tables for data (raw info) and bookings.  
6. **Slack (Optional)**  
   * For team notifications.  
     ---

     ### **1\. Configure the VAPI Booking Agent \+ Tools** (use schemas given)

1. **Create or Edit Your VAPI Agent**  
   * **Task**: Qualify the lead, then book an appointment into TALK AI’s calendar.  
   * **Process**:  
     1. Ask the caller’s name and if they’re interested in AI voice agents.  
     2. Ask for a preferred booking time.  
     3. Use `checkCalendarN8N` to check availability.  
     4. If available, use `bookCalendarN8N` to finalize the booking.  
     5. Confirm SMS details upon successful booking.  
     6. End the call with `endCall`.  
2. **Important Notes**  
   * Always check availability before booking.  
   * Never assume a day/slot is available.  
   * If the requested slot is busy, suggest the next available day.  
3. **Time Zone**  
   * Use the current time for your location (e.g., `Australia/Sydney`).  
   * Adjust the prompt and function calls for your own timezone if different.  
     ---

     ### **2\. Create an Event in Cal.com**

1. **New Event Type**  
   * Name it (e.g., “Discovery Call”).  
   * Set a duration (e.g., 15 minutes).  
   * Choose an integration (Google Calendar, Teams, etc.).  
   * Set availability (e.g., 9 a.m. – 5 p.m., Monday – Friday).  
2. **Check/Adjust Buffers & Notice**  
   * Under **Limits**, set buffers/notice times to 0 if you allow same-day or short-notice bookings.  
3. **Advanced Settings**  
   * Ensure event name can be set via an API variable (e.g., “{title}”).  
   * Toggle **Check for conflicts** to recognize calendar busy times.  
   * Add a **phone number** field under “Booking Questions” for SMS confirmations.  
4. **IDs and Keys**  
   * **Event Type ID**: Found in the event’s URL.  
   * **API Key**: Create one under **Settings → API Keys**.  
     ---

     ### **3\. Set Up the n8n Workflow**

1. **Import the Workflow**  
   * Create a new workflow in n8n.  
   * Click **Import from File** (or paste JSON if provided).  
2. **Configure Cal.com Credentials**  
   * In the relevant API call nodes, add your Cal.com API key.  
   * Insert your **Event Type ID** and **GMT offset** (e.g., \+11:00 for Sydney).  
3. **Adjust the Booking Module**  
   * Insert **Event Type ID** in the payload body.  
   * Set the **start time** offset to match your timezone.  
   * Provide a default email/phone if necessary.  
   * Update the **timezone** field (e.g., `America/New_York`).  
4. **Time Zone Adjustments**  
   * Check any **Format/Filter** or **Attempt Increment** nodes referencing time offsets (e.g., \+11:00).  
   * Change them to your local offset (e.g., \-05:00 for EST).  
     ---

     ### **4\. Connect and Configure Airtable**

1. **Create Two Tables** (if following the example)  
   * **Table 1**: Stores raw data (essential info).  
   * **Table 2**: Stores successful bookings.  
2. **Obtain and Add Airtable Credentials**  
   * Go to [https://airtable.com/create/tokens](https://airtable.com/create/tokens).  
   * Create a token with **read**, **write**, and **schema: bases:read** scopes.  
   * In n8n, add these credentials in the Airtable nodes.  
3. **Set Base and Table IDs**  
   * Locate **Base ID** and **Table ID** from your Airtable URL.  
   * In n8n, paste them into each relevant Airtable node.  
     ---

     ### **5\. Connect Twilio for SMS Confirmations**

1. **Access Twilio Console**  
   * Go to [https://console.twilio.com/](https://console.twilio.com/).  
   * Retrieve **Account SID** and **Auth Token**.  
2. **Add Twilio Credentials in n8n**  
   * In the Twilio node, enter **Account SID** and **Auth Token**.  
3. **Configure Sender Number**  
   * Change the **From** number to the one active in your Twilio account.  
     ---

     ### **6\. Connect Slack for Team Notifications (Optional)**

1. **Create or Select a Slack App**  
   * Generate or retrieve your Slack tokens.  
2. **Add Slack Credentials**  
   * In n8n, add or connect Slack under **Credentials**.  
3. **Choose a Channel/User**  
   * Decide where notifications should appear (e.g., `#sales`).  
4. **Compose Notification**  
   * Customize your message to include booking details.  
     ---

     ### **7\. Final Checks and Testing**

1. **Review Time Zones**  
   * Ensure every date/time node is correct for your timezone.  
2. **Test the Flow**  
   * Provide a requested time and confirm availability checking works.  
   * Check that a booking is created in Cal.com (and reflected in your linked calendar).  
   * Verify Airtable is updated.  
   * Ensure Twilio sends an SMS.  
   * Confirm Slack notification if configured.  
3. **Adjust as Needed**  
   * If issues arise, verify credentials, IDs, or time offsets.  
   * Confirm buffer/notice times in Cal.com don’t block short-notice bookings unless desired.  
   * 

