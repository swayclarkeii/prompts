- **📅 SECTION 2 – DAY 1 : Kickoff + Environment Setup (Full Teaching Version)**
    
    ### **🎯 Outcome by end of Day 1**
    
    A clean working environment on your **Mac** with:
    
    - VS Code ready, a project folder, Git repo on GitHub
    - Python + essential libraries installed and verified
    - .env with your API keys (OpenAI today; others later)
    - Make.com scenario created (webhook ready)
    - Google Drive/Sheets connected to Make
    - A notes.md file with your key URLs and checks
    
    ---
    
    ## **🧭 Order of Operations (quick map)**
    
    1. Create project folder → 2) Open in VS Code → 3) Verify Python/pip → 4) (Optional) create venv → 5) Install libs → 6) Initialize Git & .gitignore → 7) Create .env with API key → 8) Make.com webhook scenario → 9) Connect Google → 10) Capture everything in notes.md and validate.
    
    ---
    
    ## **🧩 Key Analogies (used throughout)**
    
    - **VS Code = workshop** (where you build)
    - **Terminal = toolbox** (where you run commands)
    - **GitHub = time machine** (undo/track your code history)
    - **.env = secret drawer** (keeps keys safe, not in code)
    - **Make.com = robot assistant** (connects apps w/o code)
    
    ---
    
    ## **🪜 Step-by-Step Instructions**
    
    ### **Step 1 – Create your project folder**
    
    **Where:** Terminal (Mac)
    
    **How:**
    
    ```
    mkdir -p ~/AI_Agency_Sprint/{scripts,data,outputs}
    cd ~/AI_Agency_Sprint
    ```
    
    **Why:** A predictable structure keeps code, data, and outputs separate (clean debugging).
    
    **Verify:**
    
    ```
    pwd
    ls -la
    ```
    
    You should see scripts/ data/ outputs/.
    
    ---
    
    ### **Step 2 – Open the folder in VS Code**
    
    **Where:** Terminal → launches VS Code
    
    **How:**
    
    ```
    code .
    ```
    
    (If code command not found: VS Code → Command Palette → “Shell Command: Install ‘code’ command in PATH” → restart terminal → run code . again.)
    
    **Why:** Work from the project root so relative paths “just work.”
    
    ---
    
    ### **Step 3 – Verify Python & pip**
    
    **Where:** Terminal (inside project root)
    
    **How:**
    
    ```
    python3 --version
    pip3 --version
    ```
    
    Expect Python **3.10+** and pip present.
    
    **If Python missing/outdated:**
    
    - Install **Homebrew** if you don’t have it:
    
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
    
    - Then:
    
    ```
    brew install python
    ```
    
    **Why:** You’ll run scripts and install libraries; versions matter.
    
    ---
    
    ### **Step 4 – (Optional but recommended) Create a virtual environment**
    
    **Where:** Terminal
    
    **How:**
    
    ```
    python3 -m venv .venv
    source .venv/bin/activate
    ```
    
    (You’ll see (.venv) prefix in terminal when active.)
    
    **Why (analogy):** A **venv** is a “sandbox kitchen”: your ingredients (libs) won’t contaminate other projects.
    
    **Deactivate later:** deactivate
    
    ---
    
    ### **Step 5 – Install essential libraries**
    
    **Where:** Terminal (with venv active, if using)
    
    **How:**
    
    ```
    pip install --upgrade pip
    pip install requests beautifulsoup4 openai python-dotenv
    ```
    
    **Why:**
    
    - requests: talk to APIs (internet calls)
    - beautifulsoup4: parse HTML (scraping)
    - openai: call OpenAI from Python
    - python-dotenv: load keys from .env (secret drawer)
    
    **Verify:**
    
    ```
    python -c "import requests, bs4, openai, dotenv; print('OK')"
    ```
    
    Should print OK.
    
    ---
    
    ### **Step 6 – Initialize Git & create a proper .gitignore**
    
    **Where:** Terminal + VS Code
    
    **How:**
    
    ```
    git init
    echo ".venv/" >> .gitignore
    echo "__pycache__/" >> .gitignore
    echo ".env" >> .gitignore
    echo ".DS_Store" >> .gitignore
    git add .
    git commit -m "Day 1: project skeleton"
    ```
    
    **Why:**
    
    - **Git = time machine** for your code.
    - .gitignore keeps secrets and junk out of commits.
    
    **Verify:**
    
    ```
    git status
    ```
    
    Should say “nothing to commit” after the commit.
    
    ---
    
    ### **Step 7 – Create**
    
    ### **.env**
    
    ### **and add your OpenAI key**
    
    **Where:** VS Code (new file in project root)
    
    **How:**
    
    Create a new file named .env with:
    
    ```
    OPENAI_API_KEY=sk-REPLACE_WITH_YOUR_KEY
    ```
    
    **Why:** Don’t hardcode secrets in scripts or commits.
    
    **Quick test script (create scripts/test_openai.py):**
    
    ```
    import os
    from dotenv import load_dotenv
    import openai
    
    load_dotenv()
    openai.api_key = os.getenv("OPENAI_API_KEY")
    
    # Simple smoketest: list models (if permissions allow) or just print key status
    print("Key loaded?", bool(openai.api_key))
    ```
    
    **Run:**
    
    ```
    python scripts/test_openai.py
    ```
    
    Expect Key loaded? True. (If False: check the key and .env location.)
    
    ---
    
    > 💡
    > 
    > 
    > **Build-vs-Buy (API key storage)**
    > 
    - 🟩 **Buy (Use .env + python-dotenv):** Safe, simple, standard. No reason to roll your own secret manager on Day 1.
    - ⚙️ **Build (Custom secrets manager):** Only if you later deploy to cloud with a managed secret service (AWS/GCP).
    - ⚠️ **Predated:** Hardcoding keys in scripts or committing .env to GitHub. Don’t do it.
    
    ---
    
    ### **Step 8 – Create your**
    
    ### **notes.md**
    
    **Where:** VS Code
    
    **How:** New file at project root: notes.md
    
    **Paste template:**
    
    ```
    # Project Notes (Day 1)
    - Project path: ~/AI_Agency_Sprint
    - Make Webhook URL: (add after Step 9)
    - Google connections: Drive/Sheets connected (Y/N)
    - GitHub repo: (URL after Step 10)
    - Keys loaded: OPENAI_API_KEY=True (from test script)
    ```
    
    **Why:** A single place to grab URLs/IDs during the sprint.
    
    ---
    
    ### **Step 9 – Make.com: create a “Catch Hook” Scenario**
    
    **Where:** Browser → Make.com
    
    **How (click path):**
    
    Make.com → Scenarios → **Create a new scenario** → Search **“Webhooks”** module → choose **“Custom webhook”** → **Add** → **Add** a new hook → name it ai_agency_intake → **Save** → **Copy** the Webhook URL.
    
    Add a second module for later (e.g., **Google Sheets → Add a Row**) but **don’t** wire it yet. We only need a working hook today.
    
    **Why (analogy):** The **webhook** is a “mail slot” your scripts or forms can post data to; Make picks it up and routes it.
    
    **Verify:**
    
    - In Make: Click **“Run once”** (listening).
    - From Terminal, send a test payload:
    
    ```
    curl -X POST "https://hook.eu1.make.com/4xdjx78tecqvm1mwxok4v9b7cnput5tk" \
      -H "Content-Type: application/json" \
      -d '{"hello":"world","source":"Day1 test"}'
    ```
    
    - You should see the incoming request appear in the Make run screen.
    
    **Record:** Paste the Webhook URL into notes.md.
    
    ---
    
    > 💡
    > 
    > 
    > **Build-vs-Buy (webhooks & orchestration)**
    > 
    - 🟩 **Buy (Make.com):** Replaces manual Flask servers + ngrok. Faster, reliable, and visual.
    - ⚙️ **Build (Custom Flask/FastAPI):** Only when you need custom logic, auth, or on-prem deployments.
    - ⚠️ **Predated:** Hand-wiring ad-hoc webhooks on localhost with ngrok for production. Great for a quick demo, not for your sprint baseline.
    
    ---
    
    ### **Step 10 – Connect Google Drive & Sheets to Make**
    
    **Where:** Browser → Make.com
    
    **How:**
    
    In the same scenario, add a **Google Drive** module → **Add** a new connection → grant access. Repeat with **Google Sheets**.
    
    **Why:** You’ll use Sheets as your default data store (simple, shareable dashboards).
    
    **Verify:**
    
    - In Make: Google Drive → List files in My Drive.
    - Choose a small range of recent files to confirm it returns results.
    
    **Record:** Update notes.md:
    
    ```
    - Google Drive connected: Yes
    - Google Sheets connected: Yes
    ```
    
    ---
    
    ### **Step 11 – Push your repo to GitHub**
    
    **Where:** Terminal + GitHub (browser)
    
    **How:**
    
    1. Create an empty repo on GitHub (no README/license).
    2. Back in Terminal:
    
    ```
    git remote add origin https://github.com/swayclarkeii/AI_Agency_Sprint.git
    git branch -M main
    git push -u origin main
    ```
    
    **Why:** Offsite backup + easy sharing.
    
    **Verify:** Open the repo URL and confirm files are visible (no .env!).
    
    **Record:** Add repo URL to notes.md.
    
    ---
    
    ## **✅ Day 1 Outputs (and how to validate)**
    
    - **Project structure:** ~/AI_Agency_Sprint/{scripts,data,outputs}
        - *Check:* ls -la shows folders.
    - **Python libs installed:** requests, beautifulsoup4, openai, python-dotenv
        - *Check:* python -c "import requests, bs4, openai, dotenv; print('OK')"
    - **.env with OpenAI key:**
        - *Check:* python scripts/test_openai.py prints Key loaded? True
    - **Make webhook URL working:**
        - *Check:* curl test shows payload in Make “Run once” panel
    - **Google connections working:**
        - *Check:* Drive/Sheets modules list files/sheets
    - **GitHub repo live:**
        - *Check:* Open repo URL; verify .env not present
    - **notes.md updated:**
        - *Check:* URLs and statuses recorded
    
    ---
    
    ## **⚠️ Guardrails (with “how to” pivots)**
    
    **Rule 1 — ⏱ 60-minute cap per blocker**
    
    - If stuck > 60 min on installs or Python:
        - **Pivot:** use **ChatGPT’s Code Interpreter** as a temporary runner.
        - *How to access:* In ChatGPT → select a GPT with **Advanced tools** → upload a small test file or paste code; run there.
        - *Why:* Don’t burn Day 1 on environment dragons.
    
    **Rule 2 — Don’t hardcode keys**
    
    - If you accidentally printed your key in code, rotate it in OpenAI immediately and update .env.
    
    **Rule 3 — Document, then move on**
    
    - Put any unresolved errors in notes.md under a “Blockers” heading. You’ll revisit on Day 3.
    
    **Rule 4 — Verify once, then proceed**
    
    - One clean run is “good enough” for Day 1. Perfection comes later.
    
    ---
    
    ## **🧪 Quick Sanity Test (5 minutes)**
    
    Run this end-to-end smoke check:
    
    1. **Local key load works:**
    
    ```
    python scripts/test_openai.py
    ```
    
    1. **Webhook accepts payload:**
    
    ```
    curl -X POST "<your-make-webhook-url>" \
      -H "Content-Type: application/json" \
      -d '{"status":"OK","from":"Day1 sanity test"}'
    ```
    
    1. **Git status clean:**
    
    ```
    git status
    ```
    
    If all three pass, Day 1 is ✅.
    
    ---
    
    ## **💡 Build-vs-Buy: Day 1 Summary (actual explanations)**
    
    - **Webhook plumbing:** **Buy** with Make.com (visual, robust) → **Build** Flask only when you need bespoke auth/logic.
    - **Secret management:** **Buy** the simple .env + python-dotenv pattern now → **Build** cloud secrets later for production.
    - **Data store:** **Buy** Google Sheets for speed → **Build** a database if/when you outgrow Sheets (volume/joins).
    - **Execution sandbox:** **Buy** ChatGPT Code Interpreter as a fallback runner → **Build** only when you need a persistent server.
    
    ---
    
    ## **📝 Reflection & Next-Day Notes (fill in Notion)**
    
    - What tripped me up today?
        - Working Github between both computer and understand how to push/pull
        - Understanding .venv and how they relate to each other
        - Learning basic terminal line commands
    - Which verification step felt unclear?
    - Any tool I should “buy” rather than “build” this week?
        - nope
    - Day 2 prep: block 2 hours for CLEAR prompts; paste course notes into outputs/day2_prompts.txt.
    
    ---
    
    If you want, I can now slot this back into your **merged Part 1** and proceed with **Days 4–7** in the same level of detail.