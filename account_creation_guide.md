# GitHub CLI Setup Guide

This guide walks you through installing and configuring the GitHub CLI (`gh`) on your laptop.  
Run these steps **after** you have created your GitHub account.

---

## What is the GitHub CLI?

The GitHub CLI (`gh`) is an official command-line tool from GitHub.  
It lets you authenticate, clone repos, create pull requests, and manage your account — all from the terminal.

---

## Mac / Linux

### Step 1 — Install the GitHub CLI

**Mac (using Homebrew):**

```bash
brew install gh
```

If you do not have Homebrew installed, install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Linux (Debian / Ubuntu):**

```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
&& sudo mkdir -p -m 755 /etc/apt/keyrings \
&& out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
&& cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```

**Linux (Fedora / RHEL / CentOS):**

```bash
sudo dnf install gh
```

### Step 2 — Verify the installation

```bash
gh --version
```

You should see output similar to:

```
gh version 2.x.x (2024-xx-xx)
```

### Step 3 — Log in to GitHub

```bash
gh auth login
```

Follow the prompts:

1. Select `GitHub.com`
2. Select `HTTPS` as the preferred protocol
3. Select `Login with a web browser`
4. Copy the one-time code shown in the terminal
5. Press Enter — your browser will open
6. Paste the code on the GitHub device activation page
7. Click **Authorize GitHub CLI**

Back in the terminal you should see:

```
Logged in as your-username
```

### Step 4 — Configure Git identity

Set your name and email so your commits are correctly attributed:

```bash
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

Verify:

```bash
git config --global --list
```

### Step 5 — Clone the workshop repository

```bash
gh repo clone [instructor-username]/task-manager
cd task-manager
python main.py
```

---

## Windows

### Step 1 — Install Git for Windows (Git Bash)

Git Bash gives you a proper Unix-style terminal on Windows, and installs Git at the same time. All commands in this guide work inside Git Bash.

**Download:**

1. Go to [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. The download starts automatically — it will be a file named something like `Git-2.x.x-64-bit.exe`
3. Run the installer

**Installer settings — what to choose at each screen:**

| Screen                                     | Recommended choice                                                    |
| ------------------------------------------ | --------------------------------------------------------------------- |
| Select Components                          | Leave all defaults ticked                                             |
| Choosing the default editor                | Select **Visual Studio Code** if installed, otherwise leave as Vim    |
| Adjusting the name of the initial branch   | Select **Override** and type `main`                                   |
| Adjusting your PATH environment            | Select **Git from the command line and also from 3rd-party software** |
| Choosing the SSH executable                | Select **Use bundled OpenSSH**                                        |
| Choosing HTTPS transport backend           | Select **Use the OpenSSL library**                                    |
| Configuring line ending conversions        | Select **Checkout Windows-style, commit Unix-style line endings**     |
| Configuring the terminal emulator          | Select **Use MinTTY (the default terminal of MSYS2)**                 |
| Choose the default behaviour of `git pull` | Select **Fast-forward or merge**                                      |
| Choose a credential helper                 | Select **Git Credential Manager**                                     |
| Extra options                              | Leave defaults                                                        |

4. Click **Install** and wait for it to complete
5. Click **Finish**

**Open Git Bash:**

- Press the **Windows key**, type `Git Bash`, and press Enter
- A terminal window with a `$` prompt will open — this is where you will run all commands for this workshop

**Verify Git is installed:**

```bash
git --version
```

Expected output:

```
git version 2.x.x.windows.x
```

---

### Step 2 — Install the GitHub CLI

Inside **Git Bash**, run:

```bash
winget install --id GitHub.cli
```

> If `winget` is not available, download the `.msi` installer manually from [https://cli.github.com](https://cli.github.com) and run it. Then close and reopen Git Bash.

**Verify the installation:**

```bash
gh --version
```

Expected output:

```
gh version 2.x.x (2024-xx-xx)
```

---

### Step 3 — Log in to GitHub

Inside **Git Bash**, run:

```bash
gh auth login
```

Follow the prompts:

1. Select `GitHub.com`
2. Select `HTTPS` as the preferred protocol
3. Select `Login with a web browser`
4. Copy the one-time code shown in the terminal
5. Press Enter — your browser will open
6. Paste the code on the GitHub device activation page
7. Click **Authorize GitHub CLI**

Back in Git Bash you should see:

```
Logged in as your-username
```

---

### Step 4 — Configure Git identity

Set your name and email so your commits are correctly attributed:

```bash
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

Verify:

```bash
git config --global --list
```

---

### Step 5 — Set the default branch name to main

If you did not set this during the installer, run:

```bash
git config --global init.defaultBranch main
```

---

### Step 6 — Clone the workshop repository

```bash
gh repo clone [instructor-username]/task-manager
cd task-manager
python main.py
```

---

## Troubleshooting

| Problem                                      | Solution                                                                        |
| -------------------------------------------- | ------------------------------------------------------------------------------- |
| `gh: command not found` after installing     | Close and reopen Git Bash — the PATH needs to refresh                           |
| `git: command not found`                     | Git Bash was not installed correctly — re-run the Git for Windows installer     |
| `winget` not recognised in Git Bash          | Use PowerShell to install the GitHub CLI, then switch back to Git Bash          |
| Browser does not open during `gh auth login` | Copy the URL printed in the terminal and paste it manually into your browser    |
| Authentication fails                         | Run `gh auth logout` then `gh auth login` again                                 |
| `git config` name/email not saving           | Make sure you include the `--global` flag                                       |
| Python not found on Windows                  | Install Python from python.org and tick "Add Python to PATH" during install     |
| Git Bash shows wrong line endings            | Re-run the Git installer and select "Checkout Windows-style, commit Unix-style" |

---

## Quick Reference — Commands Used Today

| Command                                | What it does                          |
| -------------------------------------- | ------------------------------------- |
| `gh auth login`                        | Authenticate with your GitHub account |
| `gh auth status`                       | Check if you are logged in            |
| `gh repo clone user/repo`              | Clone a repository using the CLI      |
| `git config --global user.name "..."`  | Set your commit display name          |
| `git config --global user.email "..."` | Set your commit email                 |
| `git status`                           | See what has changed                  |
| `git add .`                            | Stage all changes                     |
| `git commit -m "message"`              | Save a snapshot                       |
| `git push`                             | Upload to GitHub                      |

---

## Next Step

Once you are logged in and have cloned the repository, open `main.py` in your editor and follow the workshop activity in the slides.
