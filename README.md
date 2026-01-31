# 📝 Learning Notes CLI (`note`)

A small Bash CLI tool for creating structured learning notes as Markdown files.
Designed for developers who prefer **local files**, **Git**, and **their own workflow** over online note-taking services.

---

## ✨ Features

- 📂 Clean, predictable folder structure
- 🧱 Markdown notes with a consistent template
- 🎥 First-class support for YouTube-based learning
- 📋 List topics and notes across different sections
- 👀 View all notes within a specific topic
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
### Create a new note
```bash
note  "" [options]
```
### List all topics
```bash
note --list [section]
```
### Show notes in a topic
```bash
note --show [section] 
```

---

## 📖 Commands

### `note <topic> "<title>" [options]`
Create a new learning note.


### Arguments

| Argument | Description                                          |
| -------- | ---------------------------------------------------- |
| `topic`  | Technology or subject (e.g. `laravel`, `js`, `bash`) |
| `title`  | Note title (use quotes if it contains spaces)        |

### Options

| Option               | Description                                                               |
| -------------------- | ------------------------------------------------------------------------- |
| `--youtube <url>`    | YouTube video link                                                        |
| `--channel <value>`  | Channel in format: `"Channel Name\|https://www.youtube.com/@ChannelName"` |
| `--next <url>`       | Link to the next lesson/video                                             |
| `--project <path>`   | Local project folder path                                                 |
| `--db <name>`        | Database name (e.g. sqlite, mysql)                                        |
| `--github <url>`     | Your GitHub repository                                                    |
| `--source <value>`   | Course/source code URL or local path                                      |
| `--editor <command>` | Editor command (default: `code`)                                          |
| `-h`, `--help`       | Show help                                                                 |


### `note --list [section]`
List all topics (folders) in a section.

**Arguments:**
- `section` - Optional: `in-progress` (default), `completed`, `planned`, or `all`

**Examples:**
```bash
note --list                # list topics in in-progress
note --list completed      # list topics in completed
note --list all            # list topics in all sections
note -l planned            # short form
```

### `note --show [section] <topic>`
Show all notes within a specific topic.

**Arguments:**
- `section` - Optional: `in-progress` (default), `completed`, or `planned`
- `topic` - Topic name to show notes from

**Examples:**
```bash
note --show laravel              # show notes in in-progress/laravel
note --show planned kubernetes   # show notes in planned/kubernetes
note --show completed docker     # show notes in completed/docker
note -s python                   # short form
```

### `note --open [section] <topic> [search]` 
Open a note in your editor with fuzzy search support.
```bash
note --open [section] <topic> [search]
```
**Arguments:**
- `section` - Optional: `in-progress` (default), `completed`, or `planned`
- `topic` - Topic name containing the note
- `search` - Optional: partial filename or keywords to match

**Behavior:**
- If no search term: opens the note if only one exists, or shows interactive list
- If search term provided: filters notes by partial match (case-insensitive)
- If multiple matches: shows numbered list for interactive selection
- Opens note in configured editor (default: VS Code)

**Examples:**
```bash
# Open the only note in topic (or choose from list)
note --open laravel

# Search for specific note using keywords
note --open laravel livewire
note --open javascript basics

# Open from different sections
note --open completed docker
note --open planned kubernetes cluster

# Short form
note -o react hooks
```

**Interactive Selection Example:**
```bash
$ note --open javascript

🔍 Found 3 matching notes in 'javascript' (in-progress):

  1) JavaScript Basics
  2) JavaScript Advanced
  3) JavaScript ES6 Features

Enter number to open (or 'q' to quit): 2
✅ Opening: javascript-advanced.md
```

---

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
```markdown
# [Laravel Livewire v4](https://youtu.be/eUNWzJUvkCA)

## [YouTube - Channel Name](https://www.youtube.com/@ChannelName)

**PROJECT FOLDER:** None

**DATABASE:** sqlite

**GITHUB:** None

**SOURCE CODE:** https://github.com/channelname/livewire-course

**NEXT:** https://youtu.be/next-video-id
```

---

## 🔒 Safety & Defaults
- Notes are **never overwritten** - script exits if file exists
- Editor defaults to **VS Code** (`code`)
- If `--youtube` is provided, the note title becomes a clickable link
- All notes default to `in-progress` section

---

## 🧩 Design Philosophy
- **Local-first** - Your data stays on your machine
- **Plain text** - Markdown files you can edit anywhere
- **Git-friendly** - Perfect for version control
- **No external services** - No cloud dependencies
- **Minimal but extensible** - Simple core, easy to customize

This tool is intentionally simple and meant to evolve with your learning workflow.

---

## 💡 Workflow Tips

1. **Create notes as you learn**: Start a new note when beginning a course or tutorial
2. **List regularly**: Use `note --list` to see what you're working on
3. **Review with --show**: Use `note --show <topic>` to see all related notes
4. **Organize by sections**: Move completed topics to `completed/` folder manually
5. **Plan ahead**: Create placeholder notes in `planned/` for future learning
6. **Use with Git**: Initialize a git repo in `my-learning-notes/` to track your progress

---

## 🔮 Possible Future Improvements
- Move notes between `planned`, `in-progress`, `completed` automatically
- `note open <topic>` to quickly open a specific note
- `note search <keyword>` to search across all notes
- Auto-generate README indexes
- Templates per resource type (video, book, article, course)
- Metadata parsing and filtering
- Statistics dashboard (notes per topic, completion tracking)

---

## 📜 License

Personal tool. Use, modify, and adapt freely.