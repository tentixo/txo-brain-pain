# Beginner Step-by-Step Guide: Python + PyCharm + GitHub (macOS)

This guide walks you through creating your first Python project in **PyCharm**, setting up a virtual environment, running your code, and connecting to **GitHub**, all step-by-step for **complete beginners**.

Each step also explains **why** you're doing it—so you're not just following instructions blindly.

---

### 1. Install PyCharm (Community Edition)

**Why?** PyCharm is a powerful and beginner-friendly IDE (Integrated Development Environment) for writing, running, and managing Python code. It helps you write clean code with suggestions, debugging, and GitHub integration.

1. Visit [https://www.jetbrains.com/pycharm/download](https://www.jetbrains.com/pycharm/download)
2. Download the **Community Edition**.
3. Open the `.dmg` file and drag PyCharm into the **Applications** folder.
4. Launch PyCharm from Launchpad.

> **Note:** You may need to allow the app from **System Preferences > Security & Privacy** if macOS blocks it.

---

### 2. Create a New Python Project

**Why?** A project keeps your Python files, libraries, configurations, and Git version control organized in one place.

1. Open PyCharm.
2. Click **"New Project"**.
3. Set the **location** of your project.
4. Under **Python Interpreter**, select **"New Virtual Environment"** (PyCharm will create one for you).
5. Click **Create**.

---

### 3. Create and Save a Python Script

**Why?** Python scripts (`.py` files) contain the code you write. Every script is like a program or a set of instructions.

1. In the **Project** pane (left side), right-click the project folder.
2. Choose **New > Python File**.
3. Name your file, e.g., `hello.py` and hit **Enter**.
4. Type your first script:

```python
print("Hello, world!")
```

5. Press `Cmd + S` to save.

---

### 4. Run Your Python Code

**Why?** Running code shows you the result of your instructions. It's how you check if your script is working as expected.

#### Option 1: Green Play Button

1. Right-click on the file (`hello.py`) or click on the play button on top right  .
2. Click **Run 'hello'**.

#### Option 2: Terminal

1. Click the **Terminal** tab at the bottom.
2. Run:

```bash
python hello.py
```

> **Note:** If you see an error like `python: command not found`, use:

```bash
python3 hello.py
```

---

### 5. Create and Activate a Virtual Environment (if not done earlier)

**Why?** A virtual environment keeps your project's dependencies (installed libraries) isolated, so they don’t interfere with other projects or your system Python.

1. Go to **PyCharm > Preferences > Python Interpreter**.
2. Click the ⚙️ (gear icon) > **Add**.
3. Choose **Virtualenv Environment**.
4. Click **OK**.

PyCharm will now create and use that environment for your project.

---

### 6. Install Python Packages

**Why?** Python libraries like `requests`, `pandas`, and `flask` help you perform complex tasks without writing all the code from scratch. You install them as needed.

#### Option 1: Using PyCharm Interface

1. Go to **Preferences > Python Interpreter**.
2. Click the **+** icon.
3. Search for a package, e.g., `requests`.
4. Click **Install Package**.

#### Option 2: Using Terminal

```bash
pip install requests
```

---

### 7. Create a `.gitignore` File

**Why?** A `.gitignore` file tells Git which files/folders **not** to track. This keeps your GitHub repo clean and avoids uploading system files, temporary build files, IDE configs, and sensitive info like passwords or API keys.

1. Right-click your project folder > **New > File**.
2. Name it `.gitignore`.
3. Paste this:

```gitignore
__pycache__/
*.pyc
.env
venv/
.idea/
.DS_Store
```

> **Note:** This prevents unwanted files from being uploaded to GitHub.

---

### 8. Initialize Git in PyCharm

**Why?** Git lets you keep track of changes to your code over time. Initializing Git turns your project into a version-controlled repository.

1. Go to **VCS > Enable Version Control Integration**.
2. Select **Git** and click **OK**.

Now your project is a Git repo.

---

### 9. Connect to GitHub Repository

**Why?** GitHub is a remote service to store your code online. Connecting lets you share, back up, and collaborate on your code.

1. Create a new repo at [https://github.com](https://github.com) (do NOT initialize with README).
2. In PyCharm:

   * Go to **Git > Manage Remotes**.
   * Click **+** to add a remote.
   * Paste the GitHub HTTPS URL (e.g., `https://github.com/yourusername/yourrepo.git`).
   * Click **OK**.

---

### 10. Commit and Push Your Code

**Why?** Committing saves a snapshot of your code locally. Pushing uploads it to GitHub.

1. Click **Git** tab (bottom left) or go to **VCS > Commit**.
2. Add a commit message (e.g., `initial commit`).
3. Click **Commit and Push**.
4. Authenticate with GitHub when prompted (token-based login).

---

### 11. Basic Git Commands Cheat Sheet (in PyCharm or Terminal)

These commands can be used in PyCharm’s top menu, Git option or terminal or through the GUI menu options under Git option in Pycharm.

#### `git status`

Shows which files have been changed, staged, or are untracked.

#### `git commit -m "your message"`

Saves the current staged changes with a message.

#### `git push`

Uploads (pushes) your committed changes to GitHub.

#### `git pull`

Downloads (pulls) changes from GitHub to your local machine.
Use this before starting work if you’re collaborating.

#### `git fetch`

Checks for changes on the remote repo without applying them.

#### `git merge`

Combines changes from different branches. Use with caution if you’re just starting out.

#### `git log`

Shows a history of commits.

> **Tip:** You can also use Git GUI in PyCharm via the bottom-left Git tab, which gives visual tools for commit, push, pull, and merging.

---

### 12. Troubleshooting Common Issues

#### Interpreter Not Found

**Why it happens:** PyCharm doesn’t know which Python version to use.

* Fix: Go to **Preferences > Python Interpreter** and select or add a valid interpreter.

#### Unresolved Reference

**Why it happens:** You're using a library that hasn't been installed or is misspelled.

* Fix: Use `pip install` to install missing modules.

#### Indentation or Syntax Errors

**Why it happens:** Python requires correct indentation to work.

* Fix: Use 4 spaces (not tabs), and watch out for missing colons and brackets.

#### Git Push Fails

**Why it happens:** You may not be authenticated.

* Fix: Log in using a GitHub personal access token instead of your password.