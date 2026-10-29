# Agent Quest: Glasgow Edition - starter code

Runnable examples for the Google Agent Development Kit (ADK) workshop.
All tools are **mocked** (fake data), so the only key you need is a free Gemini API key.

```
agent-quest-starter/
├── weegie_bot/          # Levels 4-6: one agent + 3 mock tools
│   ├── __init__.py
│   ├── agent.py         # defines root_agent
│   └── .env.example
├── glasgow_guide/       # Boss level: root agent + 2 sub-agents
│   ├── __init__.py
│   ├── agent.py
│   └── .env.example
├── challenges/          # Hands-on challenge (easy / medium / hard)
└── .env.example
```

Checked against `google-adk` 2.13.0 (October 2026).

## Requirements

- **Python 3.11 or newer** (current `google-adk` releases require >=3.11; check with `python --version`)
- A Google account for a free key from Google AI Studio

## 1. Create a virtual environment and install ADK

macOS / Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install google-adk
```

Windows (PowerShell):
```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
pip install google-adk
```

Windows (Command Prompt): `.venv\Scripts\activate.bat`

## 2. Add your API key

1. Get a free key from Google AI Studio:
   1. Open https://aistudio.google.com/apikey
   2. Sign in with your Google account.
   3. If it's your first visit, accept the Google AI Studio terms.
   4. Click **Create API key**.
   5. Pick an existing Google Cloud project, or let AI Studio create a new one for you.
   6. Copy the key (a long string that starts with `AIza`) and keep it somewhere safe.
      Treat it like a password: don't share it or put it in your code.

   The free tier needs no credit card. It does have rate limits, which is plenty for this workshop.
2. Copy `weegie_bot/.env.example` to `weegie_bot/.env` (and the same for `glasgow_guide/`).
   Run these from this folder:

   macOS / Linux:
   ```bash
   cp weegie_bot/.env.example weegie_bot/.env
   cp glasgow_guide/.env.example glasgow_guide/.env
   ```

   Windows (PowerShell):
   ```powershell
   Copy-Item weegie_bot\.env.example weegie_bot\.env
   Copy-Item glasgow_guide\.env.example glasgow_guide\.env
   ```

   Windows (Command Prompt):
   ```bat
   copy weegie_bot\.env.example weegie_bot\.env
   copy glasgow_guide\.env.example glasgow_guide\.env
   ```

3. Open each `.env` file and paste your key:

```
GOOGLE_GENAI_USE_ENTERPRISE=0
GOOGLE_API_KEY=your-key-here
```

> Older ADK tutorials use `GOOGLE_GENAI_USE_VERTEXAI=FALSE`. It still works, but
> `adk create` now writes `GOOGLE_GENAI_USE_ENTERPRISE=0`. Never commit `.env`.

## 3. Run it

From **this folder** (the parent of `weegie_bot/`):

```bash
adk web            # opens the dev UI at http://localhost:8000 - pick an agent top-left
adk run weegie_bot # chat in the terminal instead
```

Try: *"Is it raining in the West End?"*, *"When's the next train from Hillhead on the inner circle?"*,
*"I'm starving in Finnieston, any chips?"*

Switch to `glasgow_guide` in the dev UI for the Boss level and watch the root agent
hand the question to `weather_agent` or `food_agent` (look for `transfer_to_agent` in the Events tab).

## 4. Make your own from scratch (optional)

```bash
adk create my_agent    # asks for model + key, writes agent.py, __init__.py, .env
```

## Challenge

Open `challenges/` and pick a tier:

| Tier | File | Task |
|------|------|------|
| ★ Easy | `easy_rate_teacake.py` | Add a snack-rating tool to Weegie Bot |
| ★★ Medium | `medium_landmark_facts.py` | Landmark lookup with error handling |
| ★★★ Hard | `hard_events_agent.py` | Add an `events_agent` sub-agent to the Glasgow Guide |

Rule of thumb for tools: clear function name, type hints, a docstring that says
what it does and what each argument means, and return a `dict` with a `status`.

## Docs

- ADK docs: https://adk.dev (formerly google.github.io/adk-docs)
- Python quickstart: https://adk.dev/get-started/python/
- Function tools: https://adk.dev/tools-custom/function-tools/
- Source: https://github.com/google/adk-python
