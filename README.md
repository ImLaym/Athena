# Athena
### A native macOS launcher for [Odysseus](https://github.com/pewdiepie-archdaemon/odysseus)

Athena is a lightweight native macOS app that wraps the Odysseus AI workspace in a proper Mac experience. It automatically starts Ollama and the Odysseus local server on launch, manages the server lifecycle, and displays the Odysseus interface in a native window — no terminal required.

---

## Features

- Automatically launches Ollama and the Odysseus server on app open
- Supports both Ollama install methods — Mac app and Homebrew
- Kills the Odysseus server cleanly on Cmd+Q
- Native loading screen while the server starts up
- One-click Odysseus update checker (git pull)
- Stop and relaunch the server from within the app
- Optional credential clearing on close for shared machines
- Displays current Athena and Odysseus versions in preferences

---

## Requirements

- macOS (Apple Silicon — M1/M2/M3)
- [Ollama](https://ollama.com) — installed either as the Mac app or via Homebrew
- [Odysseus](https://github.com/pewdiepie-archdaemon/odysseus) — cloned and set up natively at `~/odysseus`
- At least one model pulled via Ollama (e.g. `ollama pull qwen2.5-coder:14b`)

---

## Compatibility

| Setup | Supported |
|---|---|
| Ollama Mac app + Odysseus native install | ✅ |
| Ollama via Homebrew + Odysseus native install | ✅ |
| Odysseus via Docker | ❌ |
| Intel Mac | ❌ (untested) |

**Docker is not supported.** Docker on Apple Silicon cannot access the Metal GPU, which defeats the purpose of running local AI models. Athena is built around the native `start-macos.sh` install of Odysseus. If you set up Odysseus using Docker, follow the [Odysseus native install instructions](https://github.com/pewdiepie-archdaemon/odysseus) first.

---

## Installation

### Step 1 — Install Ollama

Download the Ollama Mac app from [ollama.com](https://ollama.com), or install via Homebrew:

```bash
brew install ollama
```

### Step 2 — Install Odysseus

Follow the Apple Silicon native install from the [Odysseus repository](https://github.com/pewdiepie-archdaemon/odysseus):

```bash
git clone https://github.com/pewdiepie-archdaemon/odysseus.git
cd odysseus
./start-macos.sh
```

Complete the first-time setup, create your admin account, and confirm Odysseus loads at `http://127.0.0.1:7860`. Then close the terminal — Athena will handle launching it from now on.

> **Important:** Odysseus must be cloned to your home directory as `~/odysseus`. If you cloned it somewhere else, Athena won't be able to find it.

### Step 3 — Pull a model

```bash
ollama pull qwen2.5-coder:14b
```

Or any model of your choice. See [Ollama's model library](https://ollama.com/library) for options.

### Step 4 — Download and open Athena

Download the latest `Athena.zip` from the [Releases](../../releases) page and unzip it.

> **Security notice:** Athena is not yet notarized with Apple. On first launch, macOS may show a warning that the app can't be opened. To bypass this:
> 1. Right-click `Athena.app` → **Open**
> 2. Click **Open** in the dialog that appears
>
> You only need to do this once. After that, Athena opens normally.

Move `Athena.app` to your Applications folder and add it to your Dock.

---

## First Launch

When you open Athena for the first time:

1. Athena starts Ollama if it isn't already running
2. The Odysseus server launches in the background via tmux
3. A loading screen displays while the server comes online (usually 15–30 seconds)
4. Once ready, the full Odysseus interface loads inside the app window

Log in with the admin credentials you created during Odysseus setup.

---

## Preferences

Open **Odysseus → Settings** from the menu bar.

| Setting | Description |
|---|---|
| Use Terminal Ollama | Enable if you installed Ollama via Homebrew instead of the Mac app |
| Clear login credentials on close | Forces login on every launch — useful for shared machines |
| Stop / Launch Server | Manually control the Odysseus server without quitting the app |
| Check for Odysseus Updates | Runs `git pull` on your Odysseus install and reports the result |
| Athena Version | Current version of this app |
| Odysseus Version | Current git commit of your Odysseus install |

---

## Troubleshooting

**Stuck on the loading screen:**
- Make sure Odysseus was set up correctly by running `./start-macos.sh` manually in terminal first
- Check logs at `/tmp/odysseus.log`

**"Ollama couldn't launch" error:**
- Confirm Ollama is installed — download from [ollama.com](https://ollama.com)
- If using Homebrew Ollama, enable "Use Terminal Ollama" in Odysseus → Settings

**Odysseus loads but no models appear:**
- Make sure you've pulled at least one model: `ollama pull qwen2.5-coder:14b`
- Confirm Ollama is connected in Odysseus Settings

**Gatekeeper blocks the app:**
- Right-click `Athena.app` → Open → Open

---

## Built With

- Swift / SwiftUI
- WKWebView
- Odysseus by [@pewdiepie-archdaemon](https://github.com/pewdiepie-archdaemon)

---

## License

MIT — do whatever you want with it.

---

*Athena is an independent project and is not affiliated with or endorsed by the Odysseus project.*
