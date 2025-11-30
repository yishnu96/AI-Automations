# AI Marketing Asset Generator

Automated n8n workflow that generates three AI-powered marketing visuals (Instagram Post, Instagram Story, and Ad Creative) from a single product image using OpenAI's image editing API.

## Features

- **Form-triggered workflow** - Submit product details via web form
- **AI-powered creative generation** - Creates three distinct visual formats optimized for different platforms
- **Brand customization** - Configurable brand guidelines (colors, lighting, typography, composition)
- **Auto-organized storage** - Files automatically saved to Google Drive with structured naming

## Prerequisites

- n8n instance (self-hosted or cloud)
- **Google Drive API** with OAuth credentials
- **OpenAI API** key (for image generation)
- **OpenAI API** key (for GPT-4 chat model)

## Quick Setup

### 1. Import Workflow
Import `Ad_Creatives_Agent.json` into your n8n instance.

### 2. Configure API Credentials

**Google Drive OAuth:**
- Add Google Drive OAuth2 credentials in n8n
- Grant access to your Drive folder

**OpenAI API:**
- Add OpenAI API credentials for the Chat Model node
- Add your OpenAI Bearer token in the three HTTP Request nodes:
  - Instagram Post Generator
  - Instagram Story Generator
  - Ad Creative Generator
- Replace `<Enter Open AI Token>` with `Bearer YOUR_API_KEY`

### 3. Set Google Drive Folder
- Open "Create folder" node
- Select or create a parent folder where generated assets will be stored

### 4. Customize Brand Settings
Edit the "Edit Fields" node to match your brand identity:

```json
{
  "brandName": "Your Brand",
  "brandTone": "Your visual style description",
  "colorTheme": "Your color palette",
  "backgroundStyle": "Preferred backgrounds",
  "lightingStyle": "Lighting preferences",
  "productPlacement": "Product positioning rules",
  "typographyStyle": "Font style preferences",
  "compositionGuidelines": "Layout rules"
}
```

### 5. Activate Form Trigger
- Open "On form submission" node
- Copy the **Production URL** for live use
- Share the form URL with your team

## How It Works

1. **Form Submission** → User submits product name, tagline, image, category, and benefit
2. **Brand Application** → Workflow applies custom brand guidelines
3. **AI Creative Generation** → GPT-4 agent generates three creative concepts
4. **Image Generation** → OpenAI Images Edit API creates three visual variants:
   - **Instagram Post** (1:1) - Hero asset with bold composition
   - **Instagram Story** (9:16) - Vertical mobile-optimized visual
   - **Ad Creative** (1:1) - High-impact scroll-stopping ad
5. **Storage** → All files uploaded to organized Google Drive folder

## API Details

Uses OpenAI Images Edit API endpoint:
```
POST https://api.openai.com/v1/images/edits
```

**Parameters:**
- `model`: gpt-image-1
- `prompt`: AI-generated creative direction
- `image`: User-uploaded product image
- `output_format`: png

## Form Fields

- Product Name (required)
- Product Tagline (required)
- Product Image Upload - PNG/JPG (required)
- Product Category (required)
- Highlighted Benefit (required)

## Output

Three branded marketing assets automatically saved to Google Drive:
- `Instagram Post.png`
- `Instagram Story.png`
- `Testimonial.png` (Ad Creative)

---

**Tech Stack:** n8n | OpenAI GPT-4 | OpenAI Image Edit API | Google Drive API
