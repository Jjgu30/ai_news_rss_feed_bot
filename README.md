AI News Summarizer & Telegram Bot 🤖
**
🔴 Live Demo: Experience the bot in action by messaging @ai_news_jg_bot on Telegram!**
  
  This project is an automated AI news pipeline built with n8n. It autonomously monitors high-signal YouTube channels, extracts technical specifications from video transcripts, and broadcasts concise, emoji-coded summaries to subscribers.

**💡 What It Does**
  
  Automated Intelligence The system monitors an RSS feed for new AI tech videos every hour, ensuring no major release is missed.
  
  Signal Extraction It uses DeepSeek V3 to parse unstructured transcripts, identifying open-source tools, technical parameters, and benchmarks while stripping out sponsors and fluff.
  
  Community Management The bot handles user subscriptions automatically and broadcasts formatted updates directly via a custom Telegram bot.

**🛠️ System Architecture**

  The system runs on two distinct n8n workflows that handle content processing and user management separately.
  
  1. The Content Engine (AI-RSS-Feed-bot.json)
  
  This workflow is the "brain" of the operation. It turns raw video into structured data.
  
  Trigger Detects new items via a YouTube-to-RSS feed.
  
  Ingestion (Supadata) Hits the Supadata API to instantly fetch the video transcript without downloading the media file.
  
  Analysis (DeepSeek V3) Passes the transcript through an LLM Chain with a strict prompt to extract tools (e.g., 🎵 Audio, 🖼️ Image) and filter out ads.
  
  Broadcast Retrieves the active subscriber list from Google Sheets and pushes the summary to all Chat IDs.
  
  2. The Subscriber Manager (AI-RSS-Feed-bot-subscribers.json)
  
  This workflow handles the user interaction logic.
  
  Trigger Listens for direct messages to @ai_news_jg_bot.
  
  Logic Routing The system captures the user's /start command, extracts their Chat ID, First Name, and Username, and saves them to a Google Sheet database. It also handles unsubscribe requests (/stop) and provides a fallback menu for unknown commands.
**
🧩 Tech Stack**

Orchestration: n8n LLM / Intelligence: DeepSeek V3 (via OpenRouter) Data Ingestion: Supadata (YouTube Transcripts) Database: Google Sheets Interface: Telegram Bot API
