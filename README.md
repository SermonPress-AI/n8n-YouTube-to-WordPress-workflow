# 📡 YouTube to WordPress Workflow (n8n Workflow)

This repository contains an **n8n workflow** for automating the transcription and publishing of sermon videos from YouTube to WordPress.

<img width="2303" height="667" alt="yt-to-wp-2" src="https://github.com/user-attachments/assets/7a7c30e9-1104-4a56-b1cf-ba2bb5809bef" />

## Quick Links:
- [Features](#-features)
- [Setup Instructions](-setup-instructions)
- [Usage](#-usage)
- [Cost Considerations](#-cost-considerations)
- [Security Notes](#-security-notes)
- [Troubleshooting](#-troubleshooting)
- [License](#-license)
- [Contributing](#-contributing)

## 📌 Features
- Automatically checks for new YouTube uploads on a channel.
- Downloads video audio and transcribes it using OpenAI models.
- Formats transcripts into readable paragraphs.
- Posts transcripts as **WordPress drafts** with metadata (title, description, etc.).
- Optionally logs processed videos to **Google Sheets** to prevent duplicates.


## ⚙️ Setup Instructions

### 1. Prerequisites
- An active [n8n](https://n8n.io) instance
- API keys/credentials for:
  - [**YouTube Data API**](https://developers.google.com/youtube) (for fetching channel uploads)
  - [**Supadata API**](https://supadata.ai/) (for generating transcriptions)
  - [**OpenAI API**](https://openai.com/) (for transcription formatting)
  - [**WordPress API**](https://developer.wordpress.org/rest-api/) (for posting drafts)
  - [**Google Sheets API**](https://developers.google.com/workspace/sheets) (for logging usage)


### 2. Import the Workflow
1. Copy the JSON file from this repository.
2. In your n8n instance, go to **Workflows → Import from File**.
3. Paste/upload the workflow JSON.


### 3. Configure Environment Variables
Update the following credentials in n8n:
- `YOUTUBE_API_KEY`
- `SUPADATA_API_KEY`
- `OPENAI_API_KEY`
- `WORDPRESS_USERNAME`
- `WORDPRESS_APP_PASSWORD`
- `GOOGLE_SHEETS_CREDENTIALS`


### 4. Customize Workflow Settings
- **YouTube Channel ID**: Update the node to point to the correct channel.
- **WordPress Category/Tags**: Adjust to match your site’s taxonomy.
- **Scheduling**: Configure a Cron/Trigger node to run daily/weekly.


## 🚀 Usage
Once configured, the workflow will:
1. Check for new videos on the configured YouTube channel.
2. Skip videos already logged in Google Sheets.
3. Transcribe audio into text with Supadata API.
4. Format the transcript into readable paragraphs with OpenAI.
5. Post a draft article on WordPress.


## 📊 Cost Considerations
Depending on the OpenAI model you use:
- **GPT-3.5 Turbo**: Cheapest but may occasionally summarize instead of transcribing.
- **GPT-4o Mini**: Balance between cost and reliability.
- **GPT-4o**: Most accurate formatting but higher cost and slower response.


You can configure which model to use in the workflow.


## 🔒 Security Notes
- Your API keys and n8n credentials are **not included** in this repo.
- Any references to Google Sheets or APIs in the workflow will need your own linked accounts.
- If sharing this workflow, make sure to **strip sensitive credentials**.


## 🛠 Troubleshooting
- **Workflow stuck on transcription?** Check your OpenAI model response time.
- **Duplicates appearing in WordPress?** Verify that your Google Sheets logging (or deduplication logic) is enabled.
- **WordPress authentication issues?** Ensure you’re using an **Application Password**, not your main login password.


## 📜 License
MIT License — feel free to use and adapt. See `LICENSE.md`.

---

### ✨ Contributing
Pull requests and issues are welcome. Please open an issue if you encounter bugs or have feature requests.
