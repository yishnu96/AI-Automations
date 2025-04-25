The full video resource is available here: [https://www.youtube.com/watch?v=RMOHpWAPan8](https://www.youtube.com/watch?v=RMOHpWAPan8)

This resource gives you access to all of the templates and prompts we created during my tutorial. By using them, you will be easily able to follow me along on screen and get a deeper understanding of what I’m actually doing.

## **The tools you need**

1. https://integraticus.com/share/vapi/[Vapi.a](http://Vapi.ai)i
2. https://make.com/[Make.co](http://Make.com)m
3. [Google Sheets](https://sheets.google.com/)

We may use affiliated links.

## **The **[**make.com**](http://make.com)** templates**

These are the [Make.com](http://Make.com) automation I build during the video.

[blueprint-vapi-get-assistant](https://hub.integraticus.com/wp-content/uploads/2024/04/blueprint-vapi-get-assistant.json)**[Download](https://hub.integraticus.com/wp-content/uploads/2024/04/blueprint-vapi-get-assistant.json)**[blueprint-vapi-reserve-table](https://hub.integraticus.com/wp-content/uploads/2024/04/blueprint-vapi-reserve-table.json)**[Download](https://hub.integraticus.com/wp-content/uploads/2024/04/blueprint-vapi-reserve-table.json)**

**Bonus**: Here’s a download for the Vapi Reserve Table blueprint that has the Google Calendar integration included. Please ensure to adjust the Google Calendar variables with your own calendar as they’re specific to your calendar email address.

[blueprint-vapi-reserve-table-google-calendar](https://hub.integraticus.com/wp-content/uploads/2024/05/blueprint-vapi-reserve-table-google-calendar.json)**[Download](https://hub.integraticus.com/wp-content/uploads/2024/05/blueprint-vapi-reserve-table-google-calendar.json)**

## **The Google Sheets**

Here are the Google Sheets I’ve created during the video.

- [Vapi Call Transcripts](https://docs.google.com/spreadsheets/d/1OQSe17a4MeIsCAQUE-khTYHje9RoxroYeMGHLLlbE9w/edit?usp=sharing)
- [Vapi Restaurant Leads](https://docs.google.com/spreadsheets/d/159nvDewq0edjJvIRKGG3XwBaEZGtwrDRFyCYUB-26VY/copy?usp=sharing)

## **The ChatGPT prompt to create the system prompt**

This is the prompt example I used to generate the system prompt for our assistant.

    Please rewrite the following prompt so that it serves a restaurant called "[Restaurant Name]" assistant that can reserve tables on behalf of the caller. Follow the same prompt structure but customize it so that it serves the need of the restaurant and its requirements.When asking for reserving a table, please ask the caller for the time and date, as well as the number of people that will come.Please also ask for any kind of special occasion. Here is the prompt example:[The default prompt from within Vapi]

## **The transient-based assistant JSON**

Here’s the assistant JSON from the video so you can re-use it to create your own static one, or simply for debugging.

    { "assistant": { "name": "Lisa", "voice": { "voiceId": "en-AU-KimNeural", "provider": "azure" }, "model": { "model": "gpt-3.5-turbo", "messages": [ { "role": "system", "content": "You are a voice assistant for Healthy Wrap, a vibrant restaurant located at 456 Green Leaf Boulevard, Portland, Oregon. The hours are from 11 AM to 11 PM daily, but they are closed on Mondays. The current date and time is: {{formatDate(now; "YYYY-MM-DD HH:mm:ss")}}\n\nHealthy Wrap specializes in offering nutritious and delicious wraps and salads to the Portland community.\n\nYour job involves answering queries about the restaurant and assisting callers with table reservations. When a caller wants to reserve a table, your goal is to gather the necessary information in a friendly and efficient way as follows:\n\nAsk for the caller's first name.\nInquire about the date and time they’d like to reserve a table for.\nCheck if the reservation is for a special occasion.\nAim to keep the conversation light-hearted and engaging!\nUse concise and informal language, with phrases like \"Oh, by the way,\" \"Gotcha,\" and \"Alrighty\".\nSince this is a voice interaction, keep your responses brief and conversational. Avoid overly lengthy explanations." } ], "provider": "openai", "functions": [ { "name": "ReserveTable", "async": false, "description": "Reserves a table for a given number of guests at a specific date and time.", "parameters": { "type": "object", "properties": { "date_and_time": { "type": "string", "description": "The date and time of the table reservation" }, "guest_number": { "type": "integer", "description": "The number of guests" }, "special_occasion": { "type": "string", "description": "Any special occasion if given." } }, "required": [ "date_and_time", "guest_number" ] }, "serverUrl": "WEBHOOK_ENDPOINT", "serverUrlSecret": "12345" } ], "maxTokens": 250, "temperature": 1 }, "recordingEnabled": false, "firstMessage": "Hello {{3.`0`}}, this is Lisa from Healthy Wrap, who am I talking to?", "voicemailMessage": "You've reached Healthy Wrap voicemail. Please leave a message after the beep, and we'll get back to you as soon as possible.", "endCallFunctionEnabled": true, "endCallMessage": "Thank you for contacting Healthy Wrap. Have a great day!", "transcriber": { "model": "nova-2", "language": "en", "provider": "deepgram" }, "clientMessages": [ "transcript", "hang", "function-call", "speech-update", "metadata", "conversation-update" ], "serverMessages": [ "end-of-call-report", "function-call" ], "dialKeypadFunctionEnabled": false, "endCallPhrases": [ "goodbye", "talk to you soon" ], "hipaaEnabled": false, "backgroundSound": "off", "serverUrl": "WEBHOOK_ENDPOINT", "serverUrlSecret": "12345"}}