To get started, make sure you have seen the following YouTube resource: [https://www.youtube.com/watch?v=XOVt1qHmrlg](https://www.youtube.com/watch?v=XOVt1qHmrlg)

In this resource, you will get access to all of the templates, repositories, and prompts seen during the video on how to create an AI Web Calling Assistant. You can freely use those templates without any restrictions, which also counts for the code I provide.

## **The tools you need**

1. [Vapi](https://integraticus.com/share/vapi/)
2. [Replit](https://replit.com/) (Optional if Github is used)
3. [Postman](https://postman.com/) (Optional for API Testing)
4. [JSON Editor](https://jsoneditoronline.org/) (Optional for JSON Editing)

We may use affiliated links.

## **The Code Examples**

- Replit: https://replit.com/@jannismoore/Vapi-Web-Calling[https://replit.com/@jannismoore/Vapi-Web-Callin](https://replit.com/@jannismoore/Vapi-Web-Calling)g
- GitHub: https://github.com/jannismoore/vapi-web-calling[https://github.com/jannismoore/vapi-web-callin](https://github.com/jannismoore/vapi-web-calling)g

## **How to manipulate the code snippet via ChatGTP**

I’ve shown in the video a couple of options on how you can customize the code snippets using ChatGPT. To make sure it returns the right output and content, it’s important that you fomulate your prompt correctly. Here is an example that adjusts the color of the idle button background:

    Please change the color of idle to a bright pink: const buttonConfig = { position: "bottom-right", // "bottom" | "top" | "left" | "right" | "top-right" | "top-left" | "bottom-left" | "bottom-right" offset: "40px", // decide how far the button should be from the edge width: "50px", // min-width of the button height: "50px", // height of the button idle: { // button state when the call is not active. color: `rgb(93, 254, 202)`, type: "pill", // or "round" title: "Have a quick question?", // only required in case of Pill subtitle: "Talk with our AI assistant", // only required in case of pill icon: `https://unpkg.com/lucide-static@0.321.0/icons/phone.svg`, }, loading: { // button state when the call is connecting color: `rgb(93, 124, 202)`, type: "pill", // or "round" title: "Connecting...", // only required in case of Pill subtitle: "Please wait", // only required in case of pill icon: `https://unpkg.com/lucide-static@0.321.0/icons/loader-2.svg`, }, active: { // button state when the call is in progress or active. color: `rgb(255, 0, 0)`, type: "pill", // or "round" title: "Call is in progress...", // only required in case of Pill subtitle: "End the call.", // only required in case of pill icon: `https://unpkg.com/lucide-static@0.321.0/icons/phone-off.svg`, }, };