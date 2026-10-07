<p align="center">
  <img src="assets/logo.png" alt="Agents for Claude Code, pixel-art logo with three robots on a synthwave grid" width="100%">
</p>

# Agents for Claude Code

These are the 19 subagents I run in my own Claude Code setup. Each one is a single Markdown file with a short frontmatter block and a body that tells the agent what it does, what it should leave to another agent, how to work, and what to hand back when it's done.

Claude Code reads the `description` and `not_for` lines to decide which agent fits a task. I've found the `not_for` line matters as much as the description, because most bad routing comes from a near miss: an agent that sounds right but belongs to a neighbouring job.

Some agents had notes about my own projects in them. I replaced those with a "Project context" section that lists what you should fill in for your setup.

## What's here

### App engineering

| Agent | What it does |
|---|---|
| [`macos-swiftui-engineer`](agents/macos-swiftui-engineer.md) | Builds and fixes native macOS apps in Swift and SwiftUI through SwiftPM on the command line, without Xcode. |
| [`electron-menubar-engineer`](agents/electron-menubar-engineer.md) | Works on Electron menu-bar (tray) apps: IPC between main and renderer, tray icons, windows, open at login, packaging. |
| [`apple-ui-designer`](agents/apple-ui-designer.md) | Visual redesigns in current Apple design language, plus app icons and menu-bar icons. Visual changes only, no behaviour changes. |
| [`raw-imaging-engineer`](agents/raw-imaging-engineer.md) | Image pipeline work: Core Image and Metal kernels, RAW decoding, colour science, tone curves, grain and export. |

### Claude Code setup

| Agent | What it does |
|---|---|
| [`claude-harness-engineer`](agents/claude-harness-engineer.md) | Edits Claude Code's own config: `settings.json`, the status line, `CLAUDE.md` rules, hooks and memory files. |
| [`claude-skill-builder`](agents/claude-skill-builder.md) | Builds skills in `~/.claude/skills/<name>/` with their scripts and tests, including helpers that call APIs and need secrets. |
| [`router-tooling-engineer`](agents/router-tooling-engineer.md) | Writes and tests the scripts behind a multi-provider routing setup, with unit tests and docs. |
| [`agent-librarian`](agents/agent-librarian.md) | Maintains the agent library itself. It creates an agent when nothing fit a finished task, applies your corrections to an agent, and compares agents with similar public ones when you ask. |

### Routing and delegation

These four assume a setup where Claude orchestrates and hands work to other model providers. They need the matching scripts, so treat them as examples to adapt.

| Agent | What it does |
|---|---|
| [`quota-router`](agents/quota-router.md) | Reports which providers are under their usage limits, using a state script instead of doing the math itself. |
| [`codex-runner`](agents/codex-runner.md) | Hands one bounded coding task to the Codex CLI and checks the result against a verify command. |
| [`gemini-runner`](agents/gemini-runner.md) | Does the same through the Gemini CLI and picks the cheapest model that fits the task and the free-tier budget. |
| [`model-scout`](agents/model-scout.md) | Reviews new AI models for a model catalog. It reads primary sources and community reports, then promotes or excludes each one. |

### Sessions and knowledge

| Agent | What it does |
|---|---|
| [`session-handoff-writer`](agents/session-handoff-writer.md) | Writes handoff notes so work can continue in a fresh session, and reads them back when you resume. |
| [`learning-backfill-miner`](agents/learning-backfill-miner.md) | Reads old handoff and progress notes for lessons that keep coming up, and drafts them for review. It never edits your notes directly. |
| [`second-brain-curator`](agents/second-brain-curator.md) | Maintains an Obsidian vault built as an LLM-maintained wiki, and the pipeline that feeds it. |
| [`video-insights-extractor`](agents/video-insights-extractor.md) | Watches a video and pulls out insights and to-dos, skipping anything your agents and skills already cover. |

### Everyday work

| Agent | What it does |
|---|---|
| [`spreadsheet-builder`](agents/spreadsheet-builder.md) | Creates, cleans and checks `.xlsx` and `.csv` files with openpyxl, then prints sheet names, headers and row counts so you can see what changed. |
| [`macos-system-operator`](agents/macos-system-operator.md) | Mac housekeeping: installing tools, logins that open a browser, launch agents, AppleScript, version checks after an OS update. |
| [`photo-recipe-curator`](agents/photo-recipe-curator.md) | Keeps a library of Fujifilm film-simulation recipes in a spreadsheet and a Google Drive folder of example photos for each recipe. |

## Install

Copy the agents you want into your personal agents folder:

```bash
git clone https://github.com/UribeLandscapes/claude-agents.git
cp claude-agents/agents/spreadsheet-builder.md ~/.claude/agents/
```

Or copy all of them:

```bash
cp claude-agents/agents/*.md ~/.claude/agents/
```

Start a new Claude Code session and they'll appear in the agent list. To use one in a single project, put it in that project's `.claude/agents/` folder.

Before you rely on an agent, open it and fill in its "Project context" section if it has one. Agents with an empty context section still work, but they'll spend time finding things you could have told them.

## Third-party agents

I also use agents from ECC. These copies have local changes listed in [CHANGES.md](third-party/affaan-m/ECC/CHANGES.md).

| Agent | Author | Source | License |
|---|---|---|---|
| [agent-evaluator](third-party/affaan-m/ECC/agents/agent-evaluator.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [code-explorer](third-party/affaan-m/ECC/agents/code-explorer.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [code-reviewer](third-party/affaan-m/ECC/agents/code-reviewer.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [doc-updater](third-party/affaan-m/ECC/agents/doc-updater.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [gan-evaluator](third-party/affaan-m/ECC/agents/gan-evaluator.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [gan-generator](third-party/affaan-m/ECC/agents/gan-generator.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [gan-planner](third-party/affaan-m/ECC/agents/gan-planner.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [opensource-forker](third-party/affaan-m/ECC/agents/opensource-forker.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [opensource-packager](third-party/affaan-m/ECC/agents/opensource-packager.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [opensource-sanitizer](third-party/affaan-m/ECC/agents/opensource-sanitizer.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [refactor-cleaner](third-party/affaan-m/ECC/agents/refactor-cleaner.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [security-reviewer](third-party/affaan-m/ECC/agents/security-reviewer.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |
| [tdd-guide](third-party/affaan-m/ECC/agents/tdd-guide.md) | Affaan Mustafa | [ECC](https://github.com/affaan-m/ECC) | MIT |

## Skills

The skills I use with these agents are in a separate repo: [claude-skills](https://github.com/UribeLandscapes/claude-skills).

## License

MIT for my own agents. Files under [third-party](third-party/) keep their authors' licenses.
