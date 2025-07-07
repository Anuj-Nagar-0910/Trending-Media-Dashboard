# 🎥 Trending Media Dashboard (AI-powered Video Insights)

This project uses **n8n (workflow automation)** to build an automated dashboard that:
- Fetches trending videos from [Pexels API](https://www.pexels.com/api/)
- Sends metadata to **Gemini AI (Google Generative API)** to generate descriptions and keywords
- Outputs a downloadable CSV file with AI-enhanced metadata for trending videos

---

## 🚀 Features

- ✅ Fetches top trending videos with duration filters
- 🤖 AI-generated short description and keywords using Gemini 2.0
- 📄 Generates structured CSV with thumbnails, photographer, and more
- 🐳 Fully Dockerized environment setup

---

## 🧠 Workflow Overview

```text
1. Manual Trigger ➜
2. Fetch Videos from Pexels API ➜
3. Format Data for AI ➜
4. Query Gemini AI for Tags and Description ➜
5. Parse and Extract Gemini Response ➜
6. Generate Final CSV Output
```

## 🛠 Setup Instructions

1. Clone This Repository
```bash
git clone https://github.com/your-username/trending-media-dashboard.git
cd trending-media-dashboard
```
2. Create .env File
```env
# .env file
PEXELS_API_KEY=your_pexels_api_key
GOOGLE_API_KEY=your_google_generative_api_key
```

## 🐳 Docker Setup (n8n)

Step-by-step to run the environment:
Make sure Docker is installed on your system.

1. Create docker-compose.yml
```yaml
version: '3.1'

services:
  n8n:
    image: n8nio/n8n
    container_name: n8n_trending_media
    ports:
      - 5678:5678
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=admin123
      - GENERIC_TIMEZONE=Asia/Kolkata
      - PEXELS_API_KEY=${PEXELS_API_KEY}
      - GOOGLE_API_KEY=${GOOGLE_API_KEY}
    volumes:
      - ./n8n_data:/home/node/.n8n
    restart: always
```
2. Start the container
```bash
docker-compose up -d
```
3. Access n8n in your browser
Go to: http://localhost:5678

Login using the credentials from your `.env` or `docker-compose.yml`.

## 📤 Import the Workflow

Open n8n dashboard

Click on “Import”

Upload the provided `Trending_Media_Dashboard.json` file

Set up credentials:

HTTP Header Auth for Pexels API

Header Key: `Authorization`

Header Value: `Bearer <PEXELS_API_KEY>`

No Auth needed for Gemini as it uses API key in URL

---

## **🧪 Testing the Workflow**

Click on Execute Workflow

The data will:
- Fetch trending videos
- Process through Gemini
- Produce a downloadable CSV (from the last node)

## 🔧 Customizations
| Component        | What to Change                              |
| ---------------- | ------------------------------------------- |
| Pexels API URL   | Inside **Fetch Videos** node                |
| Query Parameters | `per_page`, `min_duration`, `max_duration`  |
| Gemini Prompt    | Inside **AI Agent (Gemini)** → `text` field |
| CSV Fields       | Inside **Generate CSV** Python node         |

---

## 📂 Output Format (CSV)
| Column              | Description                  |
| ------------------- | ---------------------------- |
| video\_id           | Unique ID from Pexels        |
| video\_url          | Downloadable URL             |
| video\_thumbnail    | Preview image                |
| video\_duration     | Length in seconds            |
| video\_photographer | Name of video creator        |
| ai\_description     | Gemini-generated description |
| ai\_keywords        | Gemini-generated keywords    |
| timestamp           | UTC timestamp of generation  |

---

## 📚 Dependencies
  - n8n
  - Pexels API
  - Google Gemini Generative Language API

---

## 📢 Notes
  - Ensure you don’t exceed API quota on **Pexels** or **Gemini**
  - If you face issues with AI responses, check logs in Docker

---

🧑‍💻 Author
Anuj — GitHub

---

🪪 License
MIT License

---
