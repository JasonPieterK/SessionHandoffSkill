# SessionHandoff

A [Claude Code](https://claude.com/claude-code) skill that splits the work in your current conversation across several fresh sessions and writes one ready-to-paste handoff prompt for each.

## What it does

1. You give Claude a batch of work, for example 10 tasks (3 easy, 4 medium, 3 hard).
2. You run `/SessionHandoff`.
3. Claude asks how many sessions you want, for example 3.
4. Claude rates each task, groups them from easy to hard, and writes one self-contained prompt per session. In this example you get one prompt each for the easy, medium and hard tasks.
5. Each prompt is printed as a copy-paste block and saved to `handoffs/` in your project:

```
1st prompt (easy), saved to /home/jason/project/handoffs/session-1-easy.md
```

See [examples/example-output.md](examples/example-output.md).

## Grouping rules

- Sessions are ordered easy to hard. More sessions means finer splits.
- Tasks that touch the same code, or depend on each other, stay in the same session. If that is not possible, the overlap is flagged and each session gets its own branch.
- Asking for more sessions than tasks gives a warning and caps the number.
- A huge task can be split across sessions.
- Each prompt suggests a model that fits its difficulty.

## What each prompt contains

Summary, tasks, files, constraints, acceptance criteria, branch, and a report-back format.

## Install guide

Requires [Claude Code](https://claude.com/claude-code) and `git`.

### 1. Clone the repo

```bash
git clone https://github.com/JasonPieterK/SessionHandoffSkill.git
cd SessionHandoffSkill
```

### 2. Copy the skill into Claude Code's skills folder

**macOS**

```bash
mkdir -p ~/.claude/skills
cp -R .claude/skills/SessionHandoff ~/.claude/skills/
```

**Linux**

```bash
mkdir -p ~/.claude/skills
cp -r .claude/skills/SessionHandoff ~/.claude/skills/
```

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -Force ".claude\skills\SessionHandoff" "$env:USERPROFILE\.claude\skills\"
```

**Windows (Command Prompt)**

```bat
mkdir "%USERPROFILE%\.claude\skills"
xcopy /E /I /Y ".claude\skills\SessionHandoff" "%USERPROFILE%\.claude\skills\SessionHandoff"
```

This installs the skill for all your projects. To install it for one project only, copy the folder into that project's `.claude/skills/` instead.

### 3. Restart Claude Code and check

Restart Claude Code, then type `/SessionHandoff`. If it appears, you're done.

### Update

Run `git pull` in the cloned folder and repeat step 2.

## Usage

```
> (describe or list your tasks)
> /SessionHandoff
How many sessions do you want to split the work into?
> 3
```

You can also pass the number up front: `/SessionHandoff 3`.

## Repository layout

```
.claude/skills/SessionHandoff/SKILL.md   the skill
examples/example-output.md               sample output
LICENSE                                  MIT
```

## Contributing

Issues and pull requests are welcome. Keep `SKILL.md` short and the prompt template stable.

## License

[MIT](LICENSE)
