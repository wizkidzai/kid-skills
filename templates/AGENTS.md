# AGENTS.md

Hi, AI helper! Read this before you help with this project.

## About this project

**<Project name>** is <one or two sentences: what it does and who it's for>. Our team of kids
made it for <the challenge, class, or reason>.

## Who you are helping

Kids in elementary and middle school. Please:

- Use short sentences and simple words. Explain any new word.
- Make **one small change at a time**, then tell us what you changed and how to test it.
- Explain *why*, not just *what*, so we learn.
- Ask us a question if you are not sure what we want.
- Never pretend something works. If you didn't test it, say so.

## Where things are

| File or folder | What it does |
|---|---|
| `<file or folder>` | <what it does> |
| `skills/shared/` | Team skills shared by all our projects (a git submodule, don't edit here) |
| `skills/` | Skills just for this project |
| `requirements.md` | Our list of planned features |
| `README.md` | How to set up the project |

## Project details

The shared skills read this section, so keep it up to date.

- **Repo:** `<org>/<repo>`
- **Live site:** <URL, or "none yet">
- **Extra tools:** <tools beyond Git and GitHub CLI, each with its check command, like
  "Python 3 (`python3 --version`)". Or "none">
- **Run it:** <command, and what to open, like "`python3 -m http.server 8000`, then open
  http://localhost:8000">
- **Check it:** <command that checks for mistakes, or "none yet">
- **Try it like a user:** <what to click or do to see it working>
- **Where new features go:** <folder and files a new feature needs>
- **Deploy:** <how the project goes live after a merge, and anything only a grown-up does>

## Rules

1. **New feature? Plan it first.** If someone asks for something the project can't do yet,
   follow `skills/shared/plan-a-feature/SKILL.md`. Don't write code until the feature is in
   `requirements.md`. (Bug fixes, small tweaks, and changes to things the project already does
   don't need this.)
2. **Keep secrets secret.** This code is public. Never put passwords, tokens, or keys in any file.
3. **Make it kind and easy.** Messages people see should be friendly and simple.
4. **Use `skills/shared/devops/SKILL.md` for setup, testing, git, GitHub, and deploying.** Each
   kid works on their own branch. A grown-up reviews and merges every pull request. Never push
   to `main`.
<Add rules just for this project here.>

## Team skills

**Skills** are small instruction files that teach the AI how to do one job well. Shared skills
are in `skills/shared/<name>/SKILL.md`. Skills just for this project are in
`skills/<name>/SKILL.md`.

Before you start a task, look at the `description` at the top of each `SKILL.md` in both places.
If one fits, read the whole file and follow it. To make a new skill, use
`skills/shared/make-a-skill/SKILL.md`.
