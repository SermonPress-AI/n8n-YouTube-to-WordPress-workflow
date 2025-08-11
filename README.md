# 📡 YouTube to WordPress Workflow (n8n Workflow)

This repository contains a no-code/low-code workflow built with **n8n** as part of my internship. The goal is to automate a **YouTube-to-WordPress content publishing pipeline** for sermons or devotional media — reducing manual tasks, improving turnaround time, and increasing consistency across platforms.

<img width="2229" height="943" alt="yt-to-wp-1" src="https://github.com/user-attachments/assets/79213ea2-f960-4535-906b-18a9a564cc1d" />


---

## ✨ Project Overview

This workflow automates the process of taking a **YouTube sermon video**, retrieving its transcript, formatting it with AI, and publishing a **draft blog post** on WordPress with the embedded video and clean paragraphs, ready for final edits and publishing.

---

## 🔁 Workflow Breakdown

1. **POST Endpoint Trigger** - Receives a `POST` request containing the YouTube URL.
2. **Extract YouTube Video ID** - Parses the video ID from the submitted URL using regex.
3. **YouTube Metadata Retrieval** - Fetches the video title and embed HTML via the YouTube Data API.
4. **Transcript via Supadata API** - Uses [Supadata.ai](https://supadata.ai) to fetch the full transcript from the YouTube video directly (no downloading required).
5. **Transcript Chunking** - Breaks the video transcript into chunks to adhere to LLM input token limits.
6. **GPT-3.5 Transcript Formatting** - Sends the raw transcript to OpenAI GPT-3.5 Turbo to break text into logical, readable paragraphs.
7. **Transcript Consolidation** - Merges transcript segments into one transcript for the WordPress post.
8. **Merge YouTube and Transcript Data** - Combines YouTube metadata and transcript into one input file for WordPress.
9. **WordPress Draft Creation** - Publishes a WordPress post (as draft) using the video embed and AI-formatted transcript.

---

## ⚙️ Tools & Services Used

- **n8n** – Workflow orchestration
- **Supadata API** – Transcription directly from YouTube URL
- **OpenAI GPT-3.5 Turbo** – Formats transcript for readability
- **YouTube Data API** – Retrieves video title and embed code
- **WordPress REST API** – Creates blog post draft with embed + transcript

---

## 🧪 Usage Instructions

To trigger the workflow, send a `POST` request to the webhook URL with the following JSON payload:

```json
{
  "url": "https://youtu.be/YOUR_VIDEO_ID"
}
```

Example `curl` command:

```bash
curl -X POST https://your-n8n-instance/webhook/youtube-to-wp \
  -H "Content-Type: application/json" \
  -d '{"url": "https://youtu.be/abc123XYZ"}'
```

---

## 🚀 Setup & Deployment

1. Clone this repo and import the workflow into n8n.
2. Set API keys and credentials:
   - `YOUTUBE_API_KEY`
   - `Supadata_API_KEY`
   - `OPENAI_API_KEY`
   - `WORDPRESS_AUTH`
3. Deploy on a persistent instance (e.g., DigitalOcean, Railway, n8n cloud).

---

## 🧾 License

MIT License. See `LICENSE.md`.
