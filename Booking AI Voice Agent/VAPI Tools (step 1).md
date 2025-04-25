**Tool Schema: checkCalendarN8N**

{  
  "type": "function",  
  "function": {  
    "name": "checkCalendarN8N",  
    "async": false,  
    "description": "Use this function to check the availabilities in our calendar. ",  
    "parameters": {  
      "type": "object",  
      "properties": {  
        "requestedTime": {  
          "description": "the requested time of the user in this format in this format: 2025-02-12T11:00:00",  
          "type": "string"  
        }  
      },  
      "required": \[  
        "requestedTime"  
      \]  
    }  
  },  
  "server": {  
    "url": "\<your N8N webhook url\>",  
    "timeoutSeconds": 30  
  },  
  "async": false  
}

**Tool Schema: bookCalendarN8N**

{  
  "type": "function",  
  "function": {  
    "name": "bookCalendarN8N",  
    "async": false,  
    "description": "use this function to book an appointment into the calendar.",  
    "parameters": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "description": "the name of the caller",  
          "type": "string"  
        },  
        "reason": {  
          "description": "the reason for the call or booking",  
          "type": "string"  
        },  
        "requestedTime": {  
          "description": "the requested booking time of the user in this format: 2025-02-13T11:00:00",  
          "type": "string"  
        }  
      },  
      "required": \[  
        "requestedTime",  
        "name"  
      \]  
    }  
  },  
  "server": {  
    "url": "\<your N8N webhook url\>",  
    "timeoutSeconds": 30  
  },  
  "async": false  
}

## **Steps to Import into VAPI (Using Postman)**

1. **Open Postman**  
   Launch Postman or head to Postman’s web interface.  
2. **Create a New Request**  
   * Click **New** → **Request** (or use an existing collection).  
3. **Set Request Method and URL**  
   * Change the method to **POST**.  
   * In the address bar, enter:  
     [https://api.vapi.ai/tool](https://api.vapi.ai/tool)  
4. **Configure the Request Body**  
   * Select **Body** → **raw** → **JSON**.  
   * Paste one of the JSON schemas (for example, checkCalendarN8N) exactly as shown above into the body.  
5. **Send the Request**  
   * Click **Send** to create the tool in VAPI.  
   * If successful, you should receive a JSON response containing the newly created tool’s details (including its id, etc.).  
6. **Repeat for the Second Schema**  
   * Create another **POST** request to the same URL ([https://api.vapi.ai/tool](https://api.vapi.ai/tool)).  
   * Paste the bookCalendarN8N JSON schema into the request body.  
   * Click **Send** again.  
7. **Confirm Tool Creation**  
   * In your VAPI dashboard or via additional API calls, verify that both new tools have been created successfully.

**Note**:

* Remember to replace `<your N8N webhook url>` with your actual webhook URL.  
* If your VAPI environment requires authentication, ensure you have the proper headers or tokens set in Postman.  
  * 

