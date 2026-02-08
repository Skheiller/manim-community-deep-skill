# Manim Community Deep Skill

A Codex/agent skill that converts plain-language animation ideas into runnable **Manim Community Edition** scenes and export-ready render commands.

## What It Does

- Translates text concepts and storyboard notes into scene blueprints.
- Generates ManimCE code (`from manim import *`).
- Runs an iteration loop (layout, timing, full draft, final export).
- Produces explicit output contract: file path, render command, and tweak knobs.

## Intended Trigger

Use when a request is fundamentally:

- "Turn this explanation into Manim"
- "Convert these bullets to animation code"
- "Generate scene code and export command from this script"

Not intended for `manimlib` / ManimGL codebases.

## Structure

- `SKILL.md`: main workflow and operating contract
- `agents/openai.yaml`: UI metadata
- `references/`: blueprinting, code-generation, render/export, quality checks, troubleshooting

## Installation

Use this source value in the commands below:

```bash
SKILL_SOURCE="https://github.com/<owner>/<repo>"
```

### One-line installs (specific clients)

```bash
# Claude Code (Cloud Code)
npx -y skills add "$SKILL_SOURCE" --agent claude-code --skill manim-community-deep --global --yes

# Gemini CLI (native)
gemini skills install "$SKILL_SOURCE" --scope user --consent

# Codex
npx -y skills add "$SKILL_SOURCE" --agent codex --skill manim-community-deep --global --yes

# Anti-Gravity
npx -y skills add "$SKILL_SOURCE" --agent antigravity --skill manim-community-deep --global --yes

# Cursor
npx -y skills add "$SKILL_SOURCE" --agent cursor --skill manim-community-deep --global --yes
```

### General install (other supported agents)

Install the same skill to every agent supported by the `skills` CLI:

```bash
npx -y skills add "$SKILL_SOURCE" --skill manim-community-deep --agent '*' --global --yes
```

For any other client that supports folder-based `SKILL.md` loading, copy this repo into that client's skills directory:

```bash
AGENT_SKILLS_DIR="/path/to/your/agent/skills" && git clone "$SKILL_SOURCE" /tmp/manim-community-deep-skill && mkdir -p "$AGENT_SKILLS_DIR/manim-community-deep" && rsync -a /tmp/manim-community-deep-skill/ "$AGENT_SKILLS_DIR/manim-community-deep/"
```

### Verify installation

```bash
npx -y skills list --global
gemini skills list --all
```

## Quick Use Prompt

`Use $manim-community-deep to convert my text idea into ManimCE scene code and export-ready render commands.`

## Example Output Contract

A successful run should return:

- Scene code
- Suggested file path (for example `scenes/my_scene.py`)
- Render command (for example `manim render -qh scenes/my_scene.py MyScene`)
- Expected output path
- Short list of tweak knobs

## License

MIT
