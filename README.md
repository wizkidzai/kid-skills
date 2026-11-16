# kid-skills

Shared **skills** for Wiz Kidz student projects. A skill is a short instruction file
(`<name>/SKILL.md`) that teaches an AI helper how to do one job the team's way.

| Skill | What it does |
|---|---|
| `devops/` | Setup, running and testing, git, pull requests, deploying |
| `plan-a-feature/` | Coaches a kid to plan who, what, and why before building |
| `make-a-skill/` | Helps a kid write a new skill for their project |
| `add-analytics/` | Adds privacy-friendly visitor counts (GoatCounter, no cookies) with a private dashboard per project |
| `templates/AGENTS.md` | Starter `AGENTS.md` for a new project |

## Use it in a project

Each project adds this repo as a git submodule at `skills/shared/`:

```sh
git submodule add https://github.com/wizkidzai/kid-skills.git skills/shared
cp skills/shared/templates/AGENTS.md AGENTS.md   # then fill in every <...>
echo '@AGENTS.md' > CLAUDE.md
```

The skills are generic. They read project-specific details (repo, how to run, check, and deploy)
from the **Project details** section of the project's `AGENTS.md`. A project's own skills go in
`skills/<name>/`, next to `skills/shared/`.

To clone a project with its skills: `gh repo clone <org>/<repo> -- --recurse-submodules`.

## Change a skill

Change it here with a pull request. Then update each project:

```sh
git submodule update --remote skills/shared
git add skills/shared && git commit -m "Update shared skills"
```

Keep skills free of secrets and of anything specific to one project.
