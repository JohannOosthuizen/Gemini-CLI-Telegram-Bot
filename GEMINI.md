# Gemini-CLI Telegram Bot

This is a Python-based Telegram bot that acts as a remote interface for the Gemini CLI. It allows a user to interact with the Gemini agent from a Telegram chat, including managing project contexts and executing prompts.

## Features

- **Remote Gemini CLI Interaction:** Send prompts to the Gemini CLI from anywhere using Telegram.
- **Project Context Management:**
    - Switch between different project directories.
    - Create new projects on the fly.
- **Intelligent Context Refinement:** A user-controlled workflow to keep project requirements (`GEMINI.md`) concise and up-to-date.
- **Proactive Reminders:** The bot periodically suggests refining the context to prevent bloat.
- **Real-time File System Monitoring:** The bot monitors the current project directory for file changes (creations, deletions, modifications) and sends instant notifications to your chat, keeping you aware of the agent's activities.
- **Automatic File Content Display:** When the Gemini agent's response includes a filename in backticks (e.g., `app.py`), the bot will automatically send the content of that file to the chat if it exists.
- **File Access:** Download files from the current project context.
- **Authorization:** The bot is restricted to a single authorized Telegram user for security.
- **State Persistence:** The bot remembers the current project context for each chat across restarts.
- **Logging:** Bot activities are logged to a file for debugging and monitoring.
- **Asynchronous Gemini Calls:** Gemini CLI commands are executed as non-blocking background processes. This allows the main application to remain responsive, processing user input and other bot activities without waiting for the Gemini process to complete.

## Context Management

This bot uses a two-file system to manage project context effectively:

- **`GEMINI.md`:** This is the core requirements file for the coding agent. It's intended to be a concise, up-to-date source of truth for the project's goals. Every user prompt and accepted agent suggestion is appended to this file.
- **`project_conversation.log`:** A raw, chronological log of all interactions (user prompts and agent responses) for debugging and history.

The `/context` command and periodic reminders are designed to help you maintain the quality of the `GEMINI.md` file.

## Commands

- `/set_project <project_name> [initial_prompt]`: Sets the current working directory to an existing project. You can optionally provide an initial prompt to be executed immediately.
- `/new_project <project_name> [initial_prompt]`: Creates a new project directory and sets it as the current context. You can optionally provide an initial prompt to be executed immediately.
- `/file <filename>`: Sends the specified file from the current project directory to the chat.
- `/current_project`: Displays the path of the current project context.
- `/context`: Initiates the workflow to refine the `GEMINI.md` file. The bot will send the current version, propose an AI-consolidated version, and you can then **Accept**, **Suggest Edits**, **Decline**, or **Upload** your own version.

Any message that is not a command is treated as a prompt to the Gemini CLI. The bot will execute the prompt in the current project context and send the output back to the chat.

## Configuration

The bot is configured through a `.env` file and environment variables. The following variables are required:

- `TELEGRAM_BOT_TOKEN`: Your Telegram bot token.
- `AUTHORIZED_USER_ID`: The Telegram user ID of the authorized user.
- `PROJECTS_DIR`: The base directory where all projects are stored. This is set to a subdirectory named `projects` within the bot's directory.
- `GEMINI_SETTINGS_FILE`: The path to the Gemini settings file to be copied into new projects. This is automatically detected from your home directory (`~/.gemini/settings.json`).

## State Management

The bot's state, including the mapping of chat IDs to project paths, prompt counters for periodic reminders, and active context refinement workflows, is stored in a JSON file named `project_contexts.json`. This allows the bot to maintain context even after being restarted.

## Logging

The bot logs all its operations, including incoming messages, command executions, and errors, to `telegram-bot.log`. It also prints logs to standard output.
