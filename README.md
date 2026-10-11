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

## Install

Project only:

```bash
mkdir -p .claude/skills
cp -r .claude/skills/SessionHandoff /path/to/your/project/.claude/skills/
```

All projects:

```bash
mkdir -p ~/.claude/skills
cp -r .claude/skills/SessionHandoff ~/.claude/skills/
```

Restart Claude Code, then run `/SessionHandoff`.

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
