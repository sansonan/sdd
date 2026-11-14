# Set Up Your Development Environment
## Step-by-Step Guide: ChatGPT + OpenAI Codex

**For Windows, macOS, and Linux**

This guide explains how to set up ChatGPT and Codex for AI-powered software development.

What you'll do:

1. Prepare your ChatGPT account.
2. Install the ChatGPT desktop application (optional).
3. Install OpenAI Codex CLI.
4. Verify installation and sign in.
5. Use Codex inside VS Code or another IDE.
6. Understand permissions and project access.
7. Run your first AI-powered development task.
8. Troubleshoot common problems.

> **Keep commands current:** OpenAI may change installers, supported environments, and plan limits. Check the official Codex CLI guide before installing, especially on Windows.

---

## 1. What you need

Prepare:

- A computer running a supported version of Windows, macOS, or Linux.
- An OpenAI ChatGPT account.
- An internet connection.
- Git installed (recommended).
- A code editor such as Visual Studio Code, IntelliJ IDEA, Cursor, or another supported IDE.

### ChatGPT plan note

Codex is included with ChatGPT plans, including Free and Go, with different usage limits. Codex Cloud is not included with Free or Go. Availability and limits can change, so check the current plan details.

You do not need an OpenAI API key when signing in to Codex using your ChatGPT account.

Plan information: https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan

---

## 2. Set up ChatGPT

You can use ChatGPT through a browser or the desktop application.

### Option A: ChatGPT Web

1. Open https://chatgpt.com
2. Sign in using your OpenAI account.
3. Verify that ChatGPT opens successfully.

ChatGPT can help with learning programming concepts, software architecture discussions, requirements analysis, writing feature specifications, reviewing technical decisions, and understanding errors and logs.

### Option B: ChatGPT Desktop (optional)

1. Open https://chatgpt.com/download
2. Download the version for your operating system.
3. Install and open the application.
4. Sign in using your ChatGPT account.
5. Choose Codex when you want to work with a coding agent, where available.

The desktop app is optional. You can use Codex CLI without installing it.

---

## 3. Install Codex on macOS and Linux

### Step 1. Open Terminal

On macOS, press **Command + Space**, type **Terminal**, and press Enter.

On Linux, open your preferred terminal.

### Step 2. Install Codex CLI

Run the current official standalone installer:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

### Step 3. Restart Terminal

Close Terminal and open it again so the new command is available.

Official installation guide: https://developers.openai.com/codex/cli/

---

## 4. Install Codex on Windows

Codex supports Windows. Open the official installation guide and select its **Windows** instructions to get the current PowerShell or Windows installation method:

https://developers.openai.com/codex/cli/

Do not use Claude Code installation commands for Codex.

### Option A: Native Windows

1. Open the official Codex CLI installation page.
2. Select the **Windows** installation tab.
3. Follow the current PowerShell instructions shown there.
4. Close and reopen your terminal after installation.

### Option B: Windows Subsystem for Linux (WSL)

Use WSL when your development tools and repository are in a Linux environment.

1. Open PowerShell as Administrator and install WSL:

```powershell
wsl --install
```

2. Restart Windows if prompted and complete the Linux distribution setup.
3. Open your WSL terminal.
4. Install Codex using the Linux command from Section 3:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

5. Start Codex:

```bash
codex
```

For a WSL project, keep the repository under your Linux home directory (for example, `~/code`) for a smoother Linux development workflow. If using VS Code, install the WSL extension and open the project from the WSL terminal using `code .`.

Official WSL guide: https://learn.chatgpt.com/docs/windows/wsl

---

## 5. Check that Codex works

### Step 1. Check the installed version

Run:

```bash
codex --version
```

Expected: a Codex version number.

### Step 2. Start Codex

Run:

```bash
codex
```

The Codex terminal interface should open.

### Step 3. Sign in with ChatGPT

On first launch:

1. Choose **Sign in with ChatGPT** when prompted.
2. Your browser opens.
3. Sign in using your OpenAI account.
4. Authorize the connection.
5. Return to the terminal.

You do not need to enter your ChatGPT password into the terminal.

### Step 4. Check authentication

Inside Codex, use the current authentication and session commands listed in the CLI reference. You can also use `/status` in the interactive CLI to review session information.

CLI reference: https://developers.openai.com/codex/cli/

---

## 6. Open your project in Codex

Use your actual project directory.

### Windows PowerShell

```powershell
cd D:\smart-it-academy
git status
codex
```

### macOS / Linux

```bash
cd ~/projects/smart-it-academy
git status
codex
```

Replace the example path with the actual location of your project. Check that you are in the correct repository and review Git changes before asking Codex to edit files.

---

## 7. Understand Codex permissions

Before asking Codex to modify a project, understand its approval and sandbox settings.

- Start with a read-only review for an unfamiliar or existing repository.
- Use `/permissions` to inspect or change the permission mode.
- Review proposed file changes and diffs before accepting them.
- Do not automatically approve every command.
- Protect environment files, credentials, tokens, and production configuration.
- Never allow destructive database operations without explicit approval.
- Use Git commits or other recoverable checkpoints before significant implementation tasks.

Codex permissions and sandbox settings: https://developers.openai.com/codex/

---

## 8. Use Codex inside your code editor

### Option A: Visual Studio Code

1. Open Visual Studio Code.
2. Open Extensions.
3. Search for **Codex**.
4. Select the Codex extension published by OpenAI.
5. Click Install.
6. Open your project folder.
7. Open the Codex panel and sign in with your ChatGPT account.

Official extension listing:

https://marketplace.visualstudio.com/items?itemName=OpenAI.chatgpt

### Option B: Use Codex CLI in the integrated terminal

1. Open your project in VS Code or another IDE.
2. Open the integrated terminal.
3. Navigate to the project directory if needed.
4. Run:

```bash
codex
```

### Option C: JetBrains and other IDEs

Where a dedicated Codex integration is not available, run Codex CLI from the IDE's integrated terminal. Check the official IDE documentation for supported integrations:

https://developers.openai.com/codex/ide/

---

## 9. Your first Codex task

Do not immediately ask Codex to build a new feature. Start by understanding the existing repository.

Open Codex inside SMART IT ACADEMY and submit this prompt:

> Explain this project to me.
>
> Inspect the existing repository, including:
> - Project structure
> - Backend architecture
> - Frontend architecture
> - Database design
> - API structure
> - AGENTS.md and other applicable instructions
> - Project documentation
> - Existing development progress
>
> Do not modify any files.
> Do not run database migrations.
> Do not install dependencies.
> Do not change the Git working tree.
>
> Provide a summary of the current project architecture, completed features, incomplete features, and potential risks.
>
> This is a read-only repository assessment.

Review the response before starting implementation.

### Useful Codex commands

Inside the interactive Codex CLI, these commonly used commands are available:

- `/status` — show current session configuration.
- `/permissions` — choose what Codex is allowed to do.
- `/model` — choose the model and reasoning effort.
- `/review` — review changes and look for issues.
- `/init` — create an AGENTS.md scaffold.

**SMART IT ACADEMY note:** Do not run `/init` blindly because the repository already has project instructions. Inspect the existing AGENTS.md first to avoid overwriting or duplicating important guidance.

For the complete and current command list, consult the CLI documentation.

---

## 10. Use Codex with Spec-Driven Development (SDD)

For SMART IT ACADEMY, we will use **Hybrid SDD**:

1. Project Constitution
2. Product Vision and MVP Scope
3. Feature Specification
4. Clarify Requirements
5. Technical Planning
6. Task Breakdown
7. AI Agent Implementation
8. Feature Validation
9. Specification Convergence
10. Project Replanning
11. Next Feature Phase

Each feature must have clear requirements, acceptance criteria, implementation tasks, and verification evidence.

Keep the existing `AGENTS.md` as the project instruction source. The Project Constitution defines fundamental architectural and quality principles.

Codex must follow approved project instructions and feature specifications before modifying application code.

### Optional: GitHub Spec Kit

GitHub Spec Kit can help structure an SDD workflow.

Repository: https://github.com/github/spec-kit

Install and initialize it only after inspecting existing project files, reviewing potential conflicts, and approving an adoption plan.

---

## 11. Optional: Use ChatGPT Desktop with Codex

If you prefer a graphical interface:

1. Download ChatGPT from https://chatgpt.com/download
2. Open ChatGPT Desktop.
3. Sign in.
4. Open Codex from the available experience selector, where available.
5. Add or open your local project folder when prompted.
6. Review permissions and project context.
7. Start with a repository inspection task.

Available desktop features can vary by operating system and account.

---

## 12. Troubleshooting

### Problem: `codex` is not recognized or command not found

**Meaning:** The terminal cannot find the Codex executable.

**Fix:**

1. Close all terminal windows.
2. Open a new terminal.
3. Run `codex --version`.
4. If it still fails, check the installation and PATH using the official troubleshooting guide.

### Problem: Codex cannot sign in

**Fix:**

1. Check your internet connection.
2. Run `codex` again.
3. Follow the browser authentication process.
4. Check the current authentication options in the CLI documentation.

### Problem: Codex cannot access project files

**Fix:**

1. Confirm the current directory.
2. Check folder permissions.
3. Confirm the project is open in the intended local environment.
4. Review Codex permission and sandbox settings.

### Problem: Codex cannot detect Git

Check Git:

```bash
git --version
```

On Windows, Git for Windows is available at:

https://git-scm.com/downloads/win

### Problem: Codex usage limit reached

1. Open ChatGPT Settings or the usage dashboard.
2. Review the displayed usage and reset information.
3. Check available plan or credit options.

Do not confuse ChatGPT Codex usage limits with OpenAI API billing.

Official troubleshooting:

https://developers.openai.com/codex/

---

## 13. Official documentation

Keep these references for future use:

1. Codex overview: https://developers.openai.com/codex/
2. Codex CLI: https://developers.openai.com/codex/cli/
3. Codex IDE integration: https://developers.openai.com/codex/ide/
4. ChatGPT Desktop: https://chatgpt.com/download
5. ChatGPT and Codex plan availability: https://help.openai.com/en/articles/11369540-using-codex-with-your-chatgpt-plan
6. GitHub Spec Kit: https://github.com/github/spec-kit

---

## Quick recap

- Sign in to your ChatGPT account.
- Install ChatGPT Desktop if you prefer a graphical workspace.
- Install Codex CLI using the official installer for your operating system.
- Check installation using `codex --version`.
- Sign in using your ChatGPT account.
- Open your project folder and run `codex`.
- Install the Codex IDE extension for VS Code or use Codex CLI in another IDE's terminal.
- Start with a read-only repository inspection.
- Follow the SMART IT ACADEMY SDD workflow before implementing features.

**Remember:** ChatGPT helps you understand, plan, and learn. Codex works with your codebase as an AI coding agent. You remain the Project Owner and make the final decisions.

*Prepared: November 14, 2026. Check the official OpenAI documentation for the latest installation commands, supported environments, and plan limits.*
