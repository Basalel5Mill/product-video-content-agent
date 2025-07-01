# Product Video Content Automation Workflow

<p align="center">
  <img src="https://primary-production-2548.up.railway.app/wp-content/uploads/2025/07/product-reel-post.png" alt="Product Reel Post" width="600"/>
</p>

## Workflow Summary
A conversational, end-to-end automation that transforms your product details into a polished marketing reel in minutes. From story generation and image prompts to voiceovers, music, and final publishing, this n8n workflow handles everything.
------

## Story
> **You**: "I need a quick, engaging product video—but I have zero time to craft one."  
>
> **Workflow**: "Tell me about your product, and I’ll handle the rest!"  
>
> **You**: "Here’s my product info…"  
>
> **Workflow**: "Got it—let’s create scenes, images, voiceovers, music, and publish. Sit back, I’ve got this."

This friendly exchange turns your simple input into a captivating reel, solving the hustle of manual video production and empowering your marketing team.

---

## Contact & Front-end Integration
For seamless integration with your front-end or custom UI, reach out: **basalelr@gmail.com**

---

## Key Components & Models
- **Webhook Trigger**: Listens for incoming product data (title, text, character, tone, details).  
- **Supabase Vector Store**: Stores and retrieves your reference documents, embedded via Google Gemini text-embedding-004 (model: `text-embedding-004`).  
- **Embeddings (Google Gemini)**: Converts text into vectors for semantic search.  
- **AI Agent (Story & Scene Planner)**: Uses Google Gemini Chat (`gemini-2.5-flash-preview-05-20`) wrapped in a LangChain chainLlm to draft story summaries and scene outlines.  
- **Image AI Agent**: Prompts Replicate’s Flux Pro (model `black-forest-labs/flux-pro`) to create vivid scene images.  
- **Video Generator**: Uses RunwayML Gen-3A Turbo (`gen3a_turbo`) to animate each image into 5-second clips.  
- **Voiceover Agent**: Leverages Eleven Labs TTS (`eleven_multilingual_v2`) to produce 5-second voice lines per scene.  
- **Music Agent**: Calls Replicate Music API (version `96af46316252ddea4c6614e31861876183b59dce84bad765f38424e87919dd85`) for a 30-second background track.  
- **Google Drive Nodes**: Upload and share voiceovers and music files, returning public links.  
- **Creatomate Render**: Combines video clips, voiceovers, and music into a final video template.  
- **Publishing Agent**: Generates platform-ready titles and descriptions via LangChain for Instagram, YouTube Shorts, TikTok, and Facebook Reels.  
- **Google Sheets**: Logs metadata (record ID, video URL) for tracking.  
- **Google Cloud Storage**: Optionally saves generated images.

---

## How It Works
1. **Trigger & Embedding**  
   A Webhook receives your product details. Documents in Google Sheets are embedded and indexed in Supabase for context.  
2. **Story Creation**  
   The AI Agent fetches relevant docs, drafts a 30-word summary and six scene descriptions via Google Gemini Chat.  
3. **Image Prompts**  
   Each scene description is sent to the Image AI Agent, which calls Flux Pro to generate high-quality prompts.  
4. **Video Clips**  
   RunwayML turns each image prompt into a short video segment.  
5. **Voiceovers**  
   The Voiceover Agent crafts a script for each scene and produces MP3s via Eleven Labs.  
6. **Music Track**  
   The Music Agent generates a background track suited to your story’s vibe.  
7. **Asset Upload**  
   Voiceovers and music are uploaded to Google Drive; shareable links are captured.  
8. **Rendering**  
   Creatomate combines videos, voiceovers, and music into a cohesive reel.  
9. **Publishing**  
   The Publishing Agent writes snappy titles/descriptions and posts to social platforms via API.  
10. **Logging**  
    Final video links and metadata are recorded in Google Sheets for future reference.

---

## Detailed Node Breakdown
- **Webhook**: Receives HTTP POST with product data.  
- **Google Sheets**: Reads/writes document fields for context and logging.  
- **Embeddings Google Gemini → Supabase Vector Store**: Prepares and retrieves contextual docs.  
- **AI Agent** (LangChain chainLlm + Gemini Chat): Story & scene planning.  
- **Image AI Agent** (LangChain + Replicate HTTP Request): Flux Pro image prompts.  
- **Split Out & Wait nodes**: Manage asynchronous prediction and batching.  
- **Video Generator** (RunwayML HTTP Request): Animates images.  
- **Voiceover Agent**: LangChain → Eleven Labs TTS → SplitInBatches/Uploader.  
- **Music Agent**: LangChain → Replicate Music API → Google Drive upload.  
- **Creatomate Render**: Template rendering of final video.  
- **Publishing Agent**: LangChain-driven social copy and API posting.  
- **Google Cloud Storage** (optional): Saves image assets.  
- **Merge & Code**: Aggregates all links and fields into a final record.

---

Happy automating—no more video production headaches!  
