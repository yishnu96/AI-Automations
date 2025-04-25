**VAPI AGENT (Schema)**

*This is the raw schema for the agent used in the video. Note, some requirements will be the creation of tools; checkCalendarN8N, bookCalendarN8N (see tool schemas). Secondly, you’ll require the N8N webhook url.* 

{  
  "name": "Booking Assistant \- (N8N)",  
  "voice": {  
    "model": "eleven\_flash\_v2",  
    "voiceId": "BognUUMX6W1qmZKB2TOw",  
    "provider": "11labs",  
    "stability": 0.6,  
    "similarityBoost": 0.4,  
    "fillerInjectionEnabled": false  
  },  
  "model": {  
    "model": "gpt-4o-mini",  
    "toolIds": \[  
      "\<checkCalendarN8N toolId\>",  
      "\<bookCalendarN8N toolId\>"  
    \],  
    "messages": \[  
      {  
        "role": "system",  
        "content": "\# Role\\nYou are Sam, you're an expert booking assistant and customer service agent aimed at our business.\\n\\n\# Task\\n\#\# Qualify the lead\\n- ask their name\\nwait for response\\n- ask if they are interested in ai voice agents\\nwait for response\\n\\n\#\# Book appointment\\nwork with the caller to book an appointment into TALK AI's calendar. \\n- ask the user what time they prefer to book in an appointment? \\n- Use the 'checkCalendarN8N' function to look for availability first.\\nwait for api response\\n- use the 'bookCalendarN8N' function to finalise booking.\\nif booking successful, say \\"Thank you for booking with us, you should receive an SMS with the details and meeting link shortly\\". \\n\\n\#\# Closing call\\nonce the user has been booked in or they want to finish the call:\\n- use the 'endCall' function.\\n\\n\# Specifics\\n- Always get the availabilities first before booking\\n- use the current time as a reference for checking slots \\n- never assume a day or slot is available, always check using the function call.\\n- if a requested slot isn't available, and there is available times the following day, explicity say this.\\n\\n\# Context\\nYou work at TALK AI, a leading ai development agency. You are qualifying inbound leads that are calling in about your services. Are business hours are 9am to 5pm monday to friday. You are in a voice conversation\\n\\n\#Current Time:\\ncurrent time: {{\\"now\\" | date: \\"%b %d, %Y, %I:%M %p\\", \\"America/New\_York\\"}}\\n\\n\# Notes\\n- always steer the conversation back on track using the task and role"  
      }  
    \],  
    "provider": "openai"  
  },  
  "firstMessage": "Hello, this is Sam from Talk AI.",  
  "endCallFunctionEnabled": true,  
  "endCallMessage": "Thank you for your time today. Goodbye.",  
  "transcriber": {  
    "model": "nova-3",  
    "language": "en",  
    "provider": "deepgram"  
  },  
  "clientMessages": \[  
    "transcript"  
  \],  
  "serverMessages": \[  
    "end-of-call-report"  
  \],  
  "serverUrl": "\<your n8n webhook url\>",  
  "hipaaEnabled": false,  
  "backchannelingEnabled": false,  
  "backgroundDenoisingEnabled": false,  
  "compliancePlan": {  
    "hipaaEnabled": false,  
    "pciEnabled": false  
  },  
}

## **Steps to Import into VAPI (Using Postman)**

1. **Open Postman**  
   Launch Postman or head to Postman’s web interface.  
2. **Create a New Request**  
   * Click **New** → **Request** (or use an existing collection).  
3. **Set Request Method and URL**  
   * Change the method to **POST**.

In the address bar, enter:

`https://api.vapi.ai/assistant`

*   
4. **Configure the Request Body**  
   * Select **Body** → **raw** → **JSON**.  
   * Paste the **entire JSON schema** (exactly as shown above) into the body.  
5. **Send the Request**  
   * Click **Send** to create the agent in VAPI.  
   * If successful, you should receive a JSON response containing the newly created agent data (including its `id`, etc.).  
6. **Confirm Agent Creation**  
   * In your VAPI dashboard or via additional API calls, verify that the new agent has been created successfully.

**Note:**

* Replace all placeholder values (such as "\<checkCalendarN8N toolId\>", "\<bookCalendarN8N toolId\>", and "\<your n8n webhook url\>") with your actual IDs/URLs before sending the request.  
* Ensure you have any required authentication headers or tokens set for your VAPI account, if needed.

