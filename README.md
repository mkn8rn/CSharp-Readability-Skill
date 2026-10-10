# C# Readability Skill

A portable, single-file skill for writing, reviewing, and refactoring C# code in libraries, services, desktop apps, and games.

Early paired tests look promising: outputs produced with the skill had fewer analyzer and style warnings in all three tasks below.

| Historical task | Library with skill | Library without | Tests with skill | Tests without |
| --- | ---: | ---: | ---: | ---: |
| Framed input | 1 | 4 | 74 | 222 |
| Simulation queue | 5 | 24 | 52 | 86 |
| Desktop document | 8 | 33 | 26 | 118 |

The framed input tests had exactly one-third as many warnings (74 versus 222). The desktop document task had 34 versus 151 warnings across library and tests: about 77% fewer.

## Install and use

Copy [SKILL.md](SKILL.md) to `.agents/skills/csharp-readability/SKILL.md` in your C# project, or to `~/.agents/skills/csharp-readability/SKILL.md` for use across your Codex projects. The file is self-contained. See [official Codex skill setup](https://learn.chatgpt.com/docs/build-skills).

Then ask:

> Use $csharp-readability to review this C# code.

For other agents that support `SKILL.md`, use their skill directory.

Licensed under [AGPL-3.0-only](LICENSE). See [NOTICE](NOTICE) for copyright, contact, and source availability.
