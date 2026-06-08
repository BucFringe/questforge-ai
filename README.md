# ⚔️ QuestForge

> *An AI-powered D&D 5e quest board generator — runs entirely on your machine.*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![HTML](https://img.shields.io/badge/Built%20with-HTML%2FJS-orange)](QuestForge.html)
[![Ollama](https://img.shields.io/badge/Powered%20by-Ollama-blue)](https://ollama.ai)
[![D&D 5e](https://img.shields.io/badge/For-D%26D%205e-red)]()
[![No Install](https://img.shields.io/badge/No%20Install-Just%20Open-green)]()

QuestForge is a single HTML file that turns your local Ollama AI into a Dungeon Master's prep assistant. Describe your town, set the party's level, and generate a full adventurers' guild notice board in seconds — no internet required, no API keys, no subscription.

[![Buy Me A Coffee](https://img.buymeacoffee.com/button-api/?text=Every%20coffee%20keeps%20the%20torch&emoji=&slug=bucfringe&button_colour=FFDD00&font_colour=000000&font_family=Cookie&outline_colour=000000&coffee_colour=ffffff)](https://www.buymeacoffee.com/bucfringe)

---

## 📖 Table of Contents

- [Features](#-features)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Getting QuestForge](#getting-questforge)
  - [Recommended Models](#recommended-models)
- [How to Use](#-how-to-use)
- [Exporting to Obsidian](#-exporting-to-obsidian)
- [Screenshots](#-screenshots)
- [Known Limitations](#-known-limitations)
- [Contributing](#-contributing)
- [License](#-license)
- [Support](#-support)

---

## ✨ Features

- **Job postings** written as authentic in-world handwritten notices
- **Full DM guides** per quest — opening scene, read-aloud text, key encounters, investigation clues, atmosphere tips
- **Mid-session difficulty controls** — specific tweaks to make it harder or easier on the fly
- **Complete NPC stat blocks** in D&D 5e format — AC, HP, stats, actions, traits, equipment, and roleplaying notes
- **Faction-aware NPCs** — if the job involves the Thieves' Guild, you get a named guild member with stats
- **Loot tables** and enemy/antagonist concepts scaled to party level
- **Failure and success consequences** that ripple into future sessions
- **Fill the Board** — generates 10 varied contracts in two batches, using a TLDR of batch 1 to ensure batch 2 is distinct
- **Generation history** — last 5 generations saved to localStorage and fully restorable
- **Live streaming** — watch the AI write contracts token by token in real time
- **Obsidian export** — one `.md` file per quest, one per NPC, with YAML frontmatter and `[[wikilinks]]` already connected
- **Fully local** — all generation runs through Ollama on your machine. Your campaign stays yours.

---

## 🚀 Getting Started

### Prerequisites

Before opening QuestForge you need Ollama installed and running:

**1. Install Ollama**

Download from [ollama.ai](https://ollama.ai) and run the installer for your OS.

**2. Pull a model**

Open a terminal and run one of the following:

```bash
# Recommended — best overall output quality
ollama pull llama3.1

# Fast and good JSON compliance
ollama pull mistral

# Widely available, solid results
ollama pull llama3.2
```

**3. Start Ollama**

Ollama runs as a background service after install. If it isn't running, start it with:

```bash
ollama serve
```

---

### Getting QuestForge

**Clone the repository:**

```bash
git clone https://github.com/elliottbuckingham/questforge.git
cd questforge
```

Then open `QuestForge.html` in your browser:

```bash
# macOS
open QuestForge.html

# Windows
start QuestForge.html

# Linux
xdg-open QuestForge.html
```

No build step, no `npm install`, no server required. It's just a file.

> **Note for non-localhost use:** If Ollama is running on another machine on your network, set the `OLLAMA_ORIGINS` environment variable to allow cross-origin requests:
> ```bash
> OLLAMA_ORIGINS=* ollama serve
> ```

---

### Recommended Models

| Model | Quality | Speed | Notes |
|-------|---------|-------|-------|
| `llama3.1` | ⭐⭐⭐⭐⭐ | Medium | Best overall output and JSON compliance |
| `mistral` | ⭐⭐⭐⭐ | Fast | Very good JSON, reliable stat blocks |
| `llama3.2` | ⭐⭐⭐⭐ | Fast | Solid, widely available |
| `phi3` | ⭐⭐⭐ | Very fast | Shorter outputs, may truncate |

> Smaller models (under 7B parameters) may produce fewer NPCs or truncated stat blocks. QuestForge has a multi-stage JSON repair system to handle common model output issues, but larger models produce cleaner results.

---

## 🎲 How to Use

1. **Enter your town details** in the sidebar — name, size, and a description of notable features (port, mine, rival factions, etc.). The more detail you give, the more varied and contextual the jobs will be.

2. **Set your party** — level range (2-level increments from 1–20) and party size.

3. **Choose a model** from the dropdown — populated automatically from your installed Ollama models.

4. **Generate:**
   - **Post New Jobs** — generates the number of jobs you specify and adds them to the board
   - **Fill the Board** — generates a full 10-job spread across all difficulty tiers in two batches

5. **Browse the results** — switch between the Jobs and NPCs tabs. Click **DM Guide** on any job to expand the full session toolkit. Click **Stat Block** on any NPC to see their full D&D 5e stats.

6. **Export to Obsidian** when you're happy with the results.

---

## 📦 Exporting to Obsidian

Click any of the export buttons in the sidebar:

- **Download Job Files** — one `.md` file per quest
- **Download NPC Files** — one `.md` file per NPC  
- **Download Full ZIP** — everything in one archive, pre-organised into folders

The ZIP extracts to:
```
Town Name/
├── Quests/
│   ├── Quest - The Dark Lighthouse.md
│   └── Quest - Missing Cargo.md
└── NPCs/
    ├── NPC - Mara Duskhollow.md
    └── NPC - Gareth Thorne.md
```

Drop the folder straight into your Obsidian vault. Each file includes:
- YAML frontmatter with type, difficulty, reward value, and tags
- `[[wikilinks]]` from quests to their NPCs already populated
- Full DM guide content in structured headers
- Full stat blocks in markdown table format
- Session notes and outcome sections ready to fill in

---

## 📸 Screenshots

![The job board filled with contracts](docs/images/1.png)
*A full board generated for Ashenveil*

![DM Guide expanded](docs/images/2.png)
*Each quest includes a full DM session guide with read-aloud text and difficulty controls*

![NPC stat block](docs/images/3.png)
*Every NPC gets a complete D&D 5e stat block*

![History](docs/images/4.png)
*A full history of what is generated*

---

## ⚠️ Known Limitations

- **Smaller models** (under 7B) may produce fewer NPCs or truncated stat blocks
- **Fill the Board** makes two sequential API calls — slower models may take 2–4 minutes total
- **localStorage history** is browser-specific — clearing browser data clears generation history
- **Ollama must have CORS enabled** for non-localhost use (`OLLAMA_ORIGINS=*`)
- **JSON parsing** — QuestForge has a multi-stage repair system, but occasionally a model will produce output that can't be recovered. Regenerating usually resolves it. Larger models produce more reliable JSON.

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a PR.

The short version:
- Open an issue first to discuss the change
- Keep PRs small and focused
- Test by opening `QuestForge.html` in a browser with Ollama running
- Don't add build steps or external dependencies — the single-file philosophy is intentional

---

## 📄 License

MIT — see [LICENSE](LICENSE) for details.

---

## ☕ Support

QuestForge is free and always will be. If it's saved you some DM prep time, consider buying me a coffee!

[![Buy Me A Coffee](https://img.buymeacoffee.com/button-api/?text=Every%20coffee%20keeps%20the%20torch&emoji=&slug=bucfringe&button_colour=FFDD00&font_colour=000000&font_family=Cookie&outline_colour=000000&coffee_colour=ffffff)](https://www.buymeacoffee.com/bucfringe)
