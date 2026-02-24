# SquadOS — Project Instructions

This project uses **SquadOS**, a multi-agent orchestration framework.

## Quick Start

Type `/squados` to open the main menu, or use any of these commands:
- `/squados create` — Create a new squad
- `/squados run <name>` — Run a squad
- `/squados help` — See all commands

## Directory Structure

- `_squados/` — SquadOS core files (do not modify manually)
- `_squados/_memory/` — Persistent memory (company context, preferences)
- `squads/` — User-created squads
- `squads/{name}/output/` — Generated content and files

## How It Works

1. The `/squados` skill is the entry point for all interactions
2. The **Architect** agent creates and modifies squads
3. The **Pipeline Runner** executes squads automatically
4. Agents communicate via persona switching (inline) or subagents (background)
5. Checkpoints pause execution for user input/approval

## Rules

- Always use `/squados` commands to interact with the system
- Do not manually edit files in `_squados/core/` unless you know what you're doing
- Squad YAML files can be edited manually if needed, but prefer using `/squados edit`
- Company context in `_squados/_memory/company.md` is loaded for every squad run
