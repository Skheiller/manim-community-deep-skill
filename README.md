# Manim Idea to Export Skill

A Codex/agent skill that converts plain-language animation ideas into runnable **Manim** scenes and export-ready render commands.

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

## Practical Usage Advice (Beautiful Output)

This skill includes guidance for visual quality, not just API correctness:

- Build one clear idea per beat (avoid dense simultaneous changes).
- Make timing explicit with `run_time`, `rate_func`, and intentional pauses.
- Prefer progressive reveal (`Write`/`Create`/`LaggedStart`) over full-screen dumps.
- Use proven graph motifs (`Axes`, `NumberPlane`, `NumberLine`, `ComplexPlane`) and staged annotations.
- Iterate with a beauty-focused loop: layout -> timing -> rhythm -> final render.
- Enforce layout-fit rules (text-in-box limits, arrow-label spacing, overlap checks).
- Enforce causal animation order for process scenes (for example `L1->L2` before `L2->L3`).
- Prefer transformation continuity (show where new objects come from) over object popping.
- Use tracker-driven scenes and selective zoom/pan for stronger intuition.
- Enforce frame-fit and centering (graphs/labels stay on-screen, no accidental clipping).
- Use preview-first export: share 480p-style preview and wait for confirmation before full-quality render.
- Keep text readable on screen using reading-time pacing (`word_count / wpm * 60 + 1s`).
- Start with a mini blueprint and preference questions before detailed blueprint/code.

See `references/visual-clarity-and-aesthetics.md`, `references/animation-philosophy-directives.md`, and `references/preflight-brief-and-preferences.md` for the full playbook.

## Installation

Use this source value in the commands below:

```bash
SKILL_SOURCE="https://github.com/<owner>/<repo>"
```

### One-line installs (specific clients)

```bash
# Claude Code
npx -y skills add "$SKILL_SOURCE" --agent claude-code --skill manim-idea-to-export --global --yes

# Gemini CLI (native)
gemini skills install "$SKILL_SOURCE" --scope user --consent

# Codex
npx -y skills add "$SKILL_SOURCE" --agent codex --skill manim-idea-to-export --global --yes

# Anti-Gravity
npx -y skills add "$SKILL_SOURCE" --agent antigravity --skill manim-idea-to-export --global --yes

# Cursor
npx -y skills add "$SKILL_SOURCE" --agent cursor --skill manim-idea-to-export --global --yes
```

### General install (other supported agents)

Install the same skill to every agent supported by the `skills` CLI:

```bash
npx -y skills add "$SKILL_SOURCE" --skill manim-idea-to-export --agent '*' --global --yes
```

For any other client that supports folder-based `SKILL.md` loading, copy this repo into that client's skills directory:

```bash
AGENT_SKILLS_DIR="/path/to/your/agent/skills" && git clone "$SKILL_SOURCE" /tmp/manim-idea-to-export-skill && mkdir -p "$AGENT_SKILLS_DIR/manim-idea-to-export" && rsync -a /tmp/manim-idea-to-export-skill/ "$AGENT_SKILLS_DIR/manim-idea-to-export/"
```

### Verify installation

```bash
npx -y skills list --global
gemini skills list --all
```

## Quick Use Prompt

`Use $manim-idea-to-export to convert my text idea into Manim scene code and export-ready render commands.`

## Example Output Contract

A successful run should return:

- Scene code
- Suggested file path (for example `scenes/my_scene.py`)
- Render command (for example `manim render -qh scenes/my_scene.py MyScene`)
- Expected output path
- Short list of tweak knobs

## License

MIT
