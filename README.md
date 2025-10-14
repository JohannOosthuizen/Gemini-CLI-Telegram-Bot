# 🚀 Gemini-CLI Telegram Bot

![Python](https://img.shields.io/badge/python-3.6%2B-blue?logo=python)
![License](https://img.shields.io/badge/license-MIT-green)
![Gemini CLI](https://img.shields.io/badge/gemini--cli-required-important?logo=google)

_Remotely control a coding agent using Telegram for creating and maintaining software projects!_

---

## ✨ Features

- 🛰️ **Remote Gemini CLI Interaction:** Send prompts to the Gemini CLI from anywhere using Telegram.
- 🗣️ **Speech-to-Text:** Send voice messages, and the bot will transcribe them into prompts for the agent.
- ⚡ **Asynchronous Operation:** Gemini CLI commands run in the background—no waiting around!
- 🗂️ **Project Context Management:** Switch between project directories or create new ones on the fly using interactive menus.
- 🤖 **Intelligent Context Refinement:** Keep `GEMINI.md` concise and up-to-date with AI-powered suggestions.
- 🚀 **Remote Code Execution:** Execute scripts (`.py`, `.sh`, etc.) within the project context directly from Telegram.
- 🖥️ **Real-time File System Monitoring:** Get instant notifications when project files are created, deleted, or modified.
- 📂 **Enhanced File Previews:** Automatically view file contents in-chat when a filename is mentioned. Files are displayed with icons based on their type.
- 📥 **File Access:** Download files directly from the project context to your device.
- 🔒 **Secure:** Only an authorized Telegram user can interact with the bot.
- 💾 **State Persistence:** The bot remembers your project context across restarts.
- 📝 **Comprehensive Logging:** Activities are logged to `telegram-bot.log` for easy debugging.

---

## 🤖 How It Works

The bot runs as a long-polling service, fetching updates from the Telegram API and processing messages from the authorized user. It uses a state machine to handle multi-step operations like creating projects or executing scripts with parameters.

- **Commands:** Recognized by a `/` prefix. Interactive menus are used for selecting projects and files.
- **Prompts:** Any message that is not a command is treated as a prompt to the Gemini CLI.
- **Voice Messages:** Automatically transcribed and used as prompts.

---

## 💡 Operating Mode

- **YOLO Mode:** By default, the agent operates autonomously, taking directives from text or voice prompts.
- **Context Management:** Uses a two-file system:
  - `GEMINI.md`: The source of truth for project requirements. All prompts and agent suggestions are automatically appended here.
  - `project_conversation.log`: A raw log of all prompts and responses for historical reference.

Refine your `GEMINI.md` using the `/context` command for a high-quality project spec!

---

## ⌨️ Commands

- `/set_project` or `/p`: Select an existing project from an interactive menu or set it by name.
- `/new_project <name>`: Create a new project context.
- `/file` or `/f`: View the content of a file or select one from a menu.
- `/e`: Select a script to execute within the project, with an option to add parameters.
- `/context`: Start the AI-powered workflow to refine and consolidate your `GEMINI.md` file.
- `/current_project`: Display the path of the current project context.

---

## 🧰 Prerequisites

- Python **3.6+**
- [Gemini CLI](https://github.com/google/gemini-cli) installed and in your PATH
- Active internet connection

---

## 🚦 Installation & Setup

```bash
git clone https://github.com/JohannOosthuizen/Gemini-CLI-Telegram-Bot.git
cd Gemini-CLI-Telegram-Bot
python -m venv venv
source venv/bin/activate    # On Windows, use: venv\Scripts\activate
pip install -r requirements.txt

---


##    Pictures

![Page 1](assets/Page-1.png)

![Page 2](assets/Page-2.png)

![Page 3](assets/Page-3.png)

---

