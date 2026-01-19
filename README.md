# 🤖 AI News Summarizer & Telegram Bot

**A high-signal, automated news pipeline that filters AI noise using n8n, DeepSeek V3, and Supadata.**

![n8n](https://img.shields.io/badge/Orchestration-n8n-FF655A) ![DeepSeek](https://img.shields.io/badge/Intelligence-DeepSeek%20V3-blue) ![Supadata](https://img.shields.io/badge/Ingestion-Supadata-green) ![Telegram](https://img.shields.io/badge/Interface-Telegram-2CA5E0)

## 🔴 Live Demo
Experience the bot in action. Message **[@ai_news_jg_bot](https://t.me/ai_news_jg_bot)** on Telegram to subscribe!

## 📋 Project Overview
This repository contains the orchestration logic for a **"Zero-Fluff" AI News Aggregator**. It solves the problem of information overload by autonomously monitoring video feeds, extracting hard technical specs (parameters, benchmarks, repo links), and stripping out ads/filler.

**The Goal:** Deliver 2-sentence, emoji-coded technical summaries to mobile devices instantly, eliminating the need to watch 20-minute videos.

## 🏗️ Architecture & Logic

The system is split into two distinct **n8n workflows** to decouple content processing from user management.

### 1. The Content Engine (Intelligence)
* **File:** `AI-RSS-Feed-bot.json`
* **Function:** The core processing brain.
    * **Trigger:** Monitors YouTube RSS feeds for new uploads every hour.
    * **Ingestion:** Uses **Supadata** to fetch raw transcripts via API (bypassing video downloads).
    * **Analysis:** Sends transcripts to **DeepSeek V3** (via OpenRouter) with a strict system prompt to:
        * Extract tool names & parameters (e.g., "100M params", "Runs on CPU").
        * Identify Open Source projects.
        * **Aggressively filter** sponsors, intros, and conversational filler.
    * **Broadcast:** Pushes the cleaned summary to all active subscribers via Telegram.

### 2. The Subscriber Manager (User Ops)
* **File:** `AI-RSS-Feed-bot-subscribers.json`
* **Function:** Handles user interactions and database management.
    * **Trigger:** Listens for webhooks from the Telegram Bot API.
    * **Logic:**
        * `/start`: Onboards new users by logging their `Chat ID`, `Username`, and `First Name` into **Google Sheets**.
        * `/stop`: Removes users from the broadcast list.
        * **Fallback:** Handles unknown commands with a help menu.

## 🛠️ Tech Stack

* **Orchestrator:** n8n (Self-Hosted/Cloud)
* **LLM:** DeepSeek V3 (Chosen for high accuracy in technical extraction)
* **Ingestion:** Supadata API
* **Database:** Google Sheets (Subscriber directory)
* **Frontend:** Telegram Bot API

## 📂 Repository File Manifest

```text
├── AI-RSS-Feed-bot.json              # MAIN: Content Engine & LLM Logic
├── AI-RSS-Feed-bot-subscribers.json  # OPS: User Management & Database Logic
├── README.md                         # Documentation
