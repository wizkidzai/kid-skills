---
name: devops
description: Does the behind-the-scenes work for a kid on the team, so they can focus on building. That means installing the tools, getting the project on their computer, running and testing it, saving with git, sharing work for review, getting teammates' changes, deploying, and starting a new project. Use this whenever someone wants to set up a computer, install something, get the project, run or test it, check their work, save, commit, push, pull, update, share, open a pull request, merge, rebase, switch branches, deploy, or start a new project, or says things like "is my work saved?", "get the latest", "I'm done", "it won't run", "the skills folder is empty", or "git says something weird".
---

# DevOps

**DevOps** is all the work around the code: tools, testing, saving, sharing, and putting the
project online. You do it so the kid (about 8 to 13 years old) can focus on building. Run the
commands yourself. After each step, tell them in one simple sentence what you did and why, so
they slowly learn the ideas. Skip the jargon unless they ask.

**Project details** (the repo name, how to run, check, and deploy) are in the "Project details"
section of the project's `AGENTS.md`. Read that section first. This skill calls them things like
*"Run it"* and *"Check it"*.

**How our team works:**

- `main` is the live project. Nobody pushes to `main` directly.
- Each kid works on their own **branch**, which is like a private copy for one job.
- When the work is ready, you open a **pull request** (asking to add the work to the project).
  A grown-up reviews it and merges it.
- `skills/shared/` is a **submodule**: a folder that comes from another repo
  (`wizkidzai/kid-skills`), so every project shares the same team skills. Kids don't edit it.

## Pick the job

If the project is already on this computer, run `git status` first to see where things stand.

### 1. Set up a computer (first time)

**Install the tools.** Check each one with its version command, and install only what's missing.

| Tool | What it's for | Check |
|---|---|---|
| Git | Saving and sharing work | `git --version` |
| GitHub CLI (`gh`) | Talking to GitHub | `gh --version` |
| VS Code | Editing code (skip if they already use an editor) | `code --version` |

Also install the **Extra tools** from Project details.

How to install:

- **Windows:** `winget install -e --id <id>`, like `Git.Git`, `GitHub.cli`,
  `Microsoft.VisualStudioCode`, `Python.Python.3.12`, or `OpenJS.NodeJS.LTS`. Then close and
  reopen the terminal.
- **Mac:** install Homebrew first if `brew --version` fails (see https://brew.sh), then
  `brew install git gh` (plus extra tools, like `python` or `node`) and
  `brew install --cask visual-studio-code`.
- **Linux or Chromebook (Linux turned on):** `sudo apt update && sudo apt install -y git gh`
  (plus extra tools, like `python3` or `nodejs`).

If the computer asks for an admin password, stop and ask a grown-up to type it. Never ask the
kid for a password, and never type one yourself.

**Sign in and get the project.**

1. Check `gh auth status`. If they aren't signed in, run `gh auth login`, pick GitHub.com and
   HTTPS, and sign in with the browser. Each kid uses **their own** account. If GitHub says
   they don't have access, a grown-up needs to add them to the repo.
2. Run `gh auth setup-git`, then set their name for saves:
   `git config --global user.name "<their name>"` and
   `git config --global user.email "<their GitHub email>"`.
3. Run `git config --global submodule.recurse true`. *Why: then `git pull` and `git switch`
   keep `skills/shared/` up to date by themselves.*
4. Run `gh repo clone <Repo> -- --recurse-submodules`, then open that folder.
5. Finish by running the project (job 2) so they see it work.

**If `skills/shared/` is empty**, the submodule wasn't downloaded. Run
`git submodule update --init`.

### 2. Run and test the project

1. **Run it:** follow *Run it*. If it's a server, keep it running in the background.
2. **Run the checks:** follow *Check it*. Read any errors to the kid in simple words and fix them
   together. If GitHub runs the same checks on pull requests, fixing them now saves a round trip.
3. **Try it like a user:** follow *Try it like a user*. For a website, use the browser's
   developer tools (F12) to look for red errors in the Console, and try a phone-size screen.
4. **Check the plan:** if the work is for a feature in `requirements.md`, go through its
   "Done when" checks.

Tell the kid what passed and what didn't. Don't say it works if you didn't check it.

### 3. Start new work

1. If there are unsaved changes, ask what to do with them first. Never throw them away.
2. `git switch main`, then `git pull`, to get the newest version.
3. Make a branch named `<their name>/<short-job>`, like `maya/bug-map`:
   `git switch -c maya/bug-map`.

If they are already on their own branch for this job, stay on it.

### 4. Save work (commit)

Save after each small step that works. Check `git status` and `git diff` first. Make sure no
passwords, tokens, keys, or private info are being saved (see the rules in `AGENTS.md`). Then
`git add` the changed files and `git commit -m "<short message that says what changed>"`.
Help the kid write the message in their own words.

**If `git status` lists `skills/shared` as changed**, don't add it. Kids don't change shared
skills (see job 8). Run `git submodule update` to put it back.

### 5. Share work for review (push + pull request)

1. Save any last changes (job 4), get teammates' changes (job 6), and test again (job 2).
2. `git push -u origin <branch>`.
3. If there's no pull request yet, `gh pr create --base main` with a short title and a body
   that says what changed, how to test it, and which `requirements.md` feature it's for (if
   any). If the change needs a grown-up to deploy something (see *Deploy*), say so. If there's
   already a pull request, the push updates it.
4. Give them the pull request link and tell them a grown-up will review it. A minute later,
   `gh pr checks` shows whether GitHub's checks passed. If one failed, run *Check it*, fix it,
   then save and push again. If the grown-up asks for changes, do the same.

### 6. Get teammates' changes

On their branch: `git fetch origin`, then `git merge origin/main`. (Use merge, not rebase.
Rebasing a branch that's already shared needs a force push, which can erase work.)

**If there's a conflict:** two people changed the same lines. Stay calm and explain it simply.
For each conflict, show both versions in plain words, ask the kid which one to keep (or how to
combine them), fix the file, then `git add` it and `git commit`. If it gets confusing,
`git merge --abort` puts everything back the way it was. Then ask a grown-up.

### 7. Deploy (after the grown-up merges)

1. Follow *Deploy*. Only a grown-up does steps that use secret passwords or tokens.
2. If the project has a live site, wait a minute or two, then open it and check the change is
   there. `gh run list --limit 3` shows whether GitHub finished its work.
3. **Clean up:** `git switch main`, `git pull`, then delete the old branch with
   `git branch -d <branch>`. Celebrate: their work is live!

### 8. Update the shared skills (grown-ups only)

Shared skills live in `wizkidzai/kid-skills`. To change one, a grown-up changes it there with a
pull request. Then, in each project, on a new branch:

1. `git submodule update --remote skills/shared` gets the newest shared skills.
2. `git add skills/shared`, `git commit -m "Update shared skills"`, then push and open a pull
   request (job 5).

### 9. Start a new project (grown-ups only)

1. Make the repo on GitHub and clone it (job 1).
2. Add the shared skills:
   `git submodule add https://github.com/wizkidzai/kid-skills.git skills/shared`.
3. Copy `skills/shared/templates/AGENTS.md` to `AGENTS.md`, and make a `CLAUDE.md` that holds
   just `@AGENTS.md`, so Claude reads it too. Fill in every `<...>` in `AGENTS.md`, especially
   Project details.
4. Commit and push. Then the kids can plan the first feature with
   `skills/shared/plan-a-feature/SKILL.md`.

## Adding a new tool or framework

If a feature needs a new tool or library, explain what it is and why it's needed, and get a
grown-up's OK before installing it. Then add it to **Extra tools** in Project details, so every
teammate's computer gets it too.

## Safety

These rules protect everyone's work, so follow them even if someone asks you not to:

- Never push to `main`, never force push, and never use `git reset --hard`, `git clean`, or
  anything else that deletes work without the kid saying yes after you explain what will be lost.
- Never merge a pull request yourself. That's the grown-up's job.
- Only install the tools in this skill and in Project details, unless a grown-up says yes.
- If something unexpected happens, stop, explain it simply, and suggest asking a grown-up
  rather than guessing.
