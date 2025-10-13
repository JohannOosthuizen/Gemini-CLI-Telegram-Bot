# Gemini-CLI Telegram Bot

This is a Python-based Telegram bot that acts as a remote interface for the Gemini CLI. It allows a user to interact with the Gemini agent from a Telegram chat, including managing project contexts, executing prompts, and monitoring file system changes in real-time.

## Features

- **Remote Gemini CLI Interaction:** Send prompts to the Gemini CLI from anywhere using Telegram.
- **Asynchronous Operation:** Gemini CLI commands are executed as non-blocking background processes, allowing the bot to remain responsive.
- **Project Context Management:**
    - Switch between different project directories.
    - Create new projects on the fly.
- **Intelligent Context Refinement:** A user-controlled workflow to keep project requirements (`GEMINI.md`) concise and up-to-date.
- **Proactive Reminders:** The bot periodically suggests refining the context to prevent bloat after a certain number of prompts.
- **Real-time File System Monitoring:** The bot monitors the current project directory for file changes (creations, deletions, modifications) and sends instant notifications to your chat.
- **Automatic File Content Display:** When the Gemini agent's response includes a filename in backticks (e.g., `` `app.py` ``), the bot will automatically send the content of that file to the chat.
- **File Access:** Download files directly from the current project context.
- **Secure:** The bot is restricted to a single, authorized Telegram user ID for security.
- **State Persistence:** The bot remembers the current project context for each chat across restarts.
- **Comprehensive Logging:** Bot activities are logged to `telegram-bot.log` for debugging and monitoring.

## How It Works

The bot runs as a long-polling service that fetches updates from the Telegram API. When a message is received from the authorized user, it is processed based on whether it's a command or a prompt. Prompts are forwarded to the `gemini-cli` executable running as a background process within the selected project directory. A file system observer watches for any changes made by the agent and reports them back to the user instantly.

### Context Management

This bot uses a two-file system to manage project context effectively:

- **`GEMINI.md`:** This is the core requirements file for the coding agent. It's intended to be a concise, up-to-date source of truth for the project's goals. Every user prompt and accepted agent suggestion is appended to this file.
- **`project_conversation.log`:** A raw, chronological log of all interactions (user prompts and agent responses) for debugging and historical reference.

The `/context` command is designed to help you maintain the quality of the `GEMINI.md` file by using the AI to consolidate and refine its content.

## Prerequisites

- Python 3.6+
- The [Gemini CLI](https://github.com/google/gemini-cli) must be installed and available in your system's PATH.
- An active internet connection.

## Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Gemini-CLI-Telegram-Bot.git
    cd Gemini-CLI-Telegram-Bot
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Create a `.env` file** in the root of the project directory and add your configuration details.

## Configuration

The bot is configured through a `.env` file. The following variables are required:

-   `TELEGRAM_BOT_TOKEN`: Your Telegram bot token obtained from BotFather.
-   `AUTHORIZED_USER_ID`: Your numerical Telegram user ID. This is for security, ensuring only you can use the bot.

**Example `.env` file:**
```env
TELEGRAM_BOT_TOKEN="1234567890:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"
AUTHORIZED_USER_ID="123456789"
```

The following paths are configured automatically but can be reviewed in `app.py`:
-   `PROJECTS_DIR`: The base directory where all projects are stored. Defaults to a subdirectory named `projects`.
-   `GEMINI_SETTINGS_FILE`: The path to the Gemini settings file (`~/.gemini/settings.json`) to be copied into new projects.

## Usage

To start the bot, simply run the `app.py` script:
```bash
python app.py
```
The bot will start polling for messages. You can interact with it from the Telegram chat associated with your `AUTHORIZED_USER_ID`.

## Commands

-   `/set_project <project_name> [initial_prompt]`: Sets the current working directory to an existing project. You can optionally provide an initial prompt to be executed immediately.
-   `/new_project <project_name> [initial_prompt]`: Creates a new project directory and sets it as the current context.
-   `/file <filename>`: Sends the specified file from the current project directory to the chat.
-   `/current_project`: Displays the path of the current project context.
-   `/context`: Initiates the workflow to refine the `GEMINI.md` file. The bot will send the current version, propose an AI-consolidated version, and you can then **Accept**, **Suggest Edits**, **Decline**, or **Upload** your own version.

Any message that is not a command is treated as a prompt to the Gemini CLI.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
