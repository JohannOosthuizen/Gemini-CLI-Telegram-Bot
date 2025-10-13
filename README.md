# 🚀 Gemini-CLI Telegram Bot

![Python](https://img.shields.io/badge/python-3.6%2B-blue?logo=python)
![License](https://img.shields.io/badge/license-MIT-green)
![Gemini CLI](https://img.shields.io/badge/gemini--cli-required-important?logo=google)

_Remotely control a coding agent using Telegram for creating and maintaining software projects!_

---

## ✨ Features

- 🛰️ **Remote Gemini CLI Interaction:**  
  Send prompts to the Gemini CLI from anywhere using Telegram.
- ⚡ **Asynchronous Operation:**  
  Gemini CLI commands run in the background—no waiting around!
- 🗂️ **Project Context Management:**  
  Switch between project directories or create new ones on the fly.
- 🤖 **Intelligent Context Refinement:**  
  Keep `GEMINI.md` concise and up-to-date with AI suggestions.
- ⏰ **Proactive Reminders:**  
  The bot suggests refining the context after a set number of prompts.
- 🖥️ **Real-time File System Monitoring:**  
  Get instant notifications when project files change.
- 📂 **Automatic File Content Display:**  
  The bot auto-sends file contents when a filename is referenced.
- 📥 **File Access:**  
  Download files directly from Telegram.
- 🔒 **Secure:**  
  Only an authorized Telegram user can interact with the bot.
- 💾 **State Persistence:**  
  The bot remembers your project context across restarts.
- 📝 **Comprehensive Logging:**  
  Activities are logged to `telegram-bot.log`.

---

## 🛠 How It Works

The bot runs as a long-polling service, fetching updates from the Telegram API and processing messages from the authorized user. Commands are recognized by a `/` prefix; all other messages are sent as prompts to the Gemini CLI.

---

## 💡 Operating Mode

- **YOLO Mode:**  
  By default, the agent operates autonomously, taking directives from the `/requirement` command.
- **Context Management:**  
  Uses a two-file system:
  - `GEMINI.md`: The source of truth for project requirements.
  - `project_conversation.log`: A raw log of all prompts and responses.

Refine your `GEMINI.md` using the `/context` command for a high-quality project spec!

---

## 🧰 Prerequisites

- Python **3.6+**
- [Gemini CLI](https://github.com/google/gemini-cli) installed and in your PATH
- Active internet connection

---

## 🚦 Installation & Setup

```bash
git clone https://github.com/your-username/Gemini-CLI-Telegram-Bot.git
cd Gemini-CLI-Telegram-Bot
python -m venv venv
source venv/bin/activate    # On Windows, use: venv\Scripts\activate
pip install -r requirements.txt
