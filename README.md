# 📝 Learning Notes CLI (`note`)

A small Bash CLI tool for creating structured learning notes as Markdown files.
Designed for developers who prefer **local files**, **Git**, and **their own workflow** over online note-taking services.

---

## ✨ Features

- 📂 Clean, predictable folder structure
- 🧱 Markdown notes with a consistent template
- 🎥 First-class support for YouTube-based learning
- ✏️ Open notes immediately in your editor
- 🔧 Editor is configurable (VS Code by default)
- 🚫 Safe by default (no overwriting existing notes)

---

## 📁 Notes Structure

All notes are stored locally under:

```
my-learning-notes/
├── README.md
├── in-progress/ # default location for new notes
│ └── <topic>/
│ └── <slug>.md
├── completed/
├── planned/
├── resources/
├── templates/
└── private/
```

By default, new notes are created in:
```~/Desktop/my-learning-notes/in-progress/<topic>/<slug>.md```



---

## 🚀 Installation

1. Save the script as `note`
2. Move it to a directory in your `$PATH`, for example:

```bash
sudo mv note /usr/local/bin/note
sudo chmod +x /usr/local/bin/note
```
3. Verify installation:
```bash
note --help
```

## 🧠 Usage
```bash
note <topic> "<title>" [options]
```
### Arguments

| Argument | Description                                          |
| -------- | ---------------------------------------------------- |
| `topic`  | Technology or subject (e.g. `laravel`, `js`, `bash`) |
| `title`  | Note title (use quotes if it contains spaces)        |

### Options

| Option               | Description                          |                                                                    |
| -------------------- | ------------------------------------ | ------------------------------------------------------------------ |
| `--youtube <url>`    | YouTube video link                   |                                                                    |
| `--channel <value>`  | Channel in format: `"Channel Name    | [https://youtube.com/@channel"`](https://youtube.com/@channel%22`) |
| `--next <url>`       | Link to the next lesson/video        |                                                                    |
| `--project <path>`   | Local project folder path            |                                                                    |
| `--db <name>`        | Database name (e.g. sqlite, mysql)   |                                                                    |
| `--github <url>`     | Your GitHub repository               |                                                                    |
| `--source <value>`   | Course/source code URL or local path |                                                                    |
| `--editor <command>` | Editor command (default: `code`)     |                                                                    |
| `-h`, `--help`       | Show help                            |                                                                    |

## 🧪 Examples

### Basic note
```bash
note bash "Bash scripting basics"
```
### YouTube-based course note
```bash
note laravel "Laravel Livewire v4" \
  --youtube https://youtu.be/eUNWzJUvkCA \
  --channel "Channel Name|https://www.youtube.com/@ChannelName"
```
### With source code and Git auto-commit
```bash
note laravel "Laravel Livewire v4" \
  --youtube https://youtu.be/eUNWzJUvkCA \
  --channel "Channel Name|https://www.youtube.com/@ChannelName" \
  --source https://github.com/channelname/livewire-course \
```
### Use a different editor
```bash
note bash "Sed & Awk" --editor nano
```

## 📝 Generated Markdown Example

# [Laravel Livewire v4](https://youtu.be/eUNWzJUvkCA)

## [YouTube - Channel Name](https://www.youtube.com/@ChannelName)

**PROJECT FOLDER:** None

**DATABASE:** sqlite

**GITHUB:** None

**SOURCE CODE:** https://github.com/channelname/livewire-course

## 🔒 Safety & Defaults
- Notes are **never overwritten**
- Git commits are **opt-in** (`--git`)
- Editor defaults to **VS Code**
- If `--youtube` is provided, the note title becomes a clickable link

## 🧩 Design Philosophy
- Local-first
- Plain text (Markdown)
- Git-friendly
- No external services
- Minimal but extensible

This tool is intentionally simple and meant to evolve with your learning workflow.

## 🔮 Possible Future Improvements
- Move notes between `planned`, `in-progress`, `completed`
- `note list`, `note open`
- Auto-generate README indexes
- Templates per resource type (video, book, article)
- Metadata parsing / search

## 📜 License

Personal tool. Use, modify, and adapt freely.