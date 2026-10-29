# The project files that tell an agent how to work

**Covers:** Repo, CLAUDE.md, CLAUDE, AGENTS.md, README.md, README, LICENSE

## A new colleague every morning {#overview}
An AI coding agent starts each session knowing nothing about your project. It cannot see what you decided last week, and it does not know your naming style or which commands run the tests. A human colleague would pick this up over time. An agent needs it written down. A handful of plain text files at the top of your project give it that background, and they help human readers too.

## Repo {#repo}
A repo, short for repository, is the folder that holds a whole project: its code, its settings and the full history of changes, tracked by Git. Everything an agent needs to understand the project should be inside it, because that is what the agent can see.

Keeping a project in a repo also gives you a safety net. If the agent makes a mess, you can compare against the saved history and go back.

## CLAUDE.md {#claude-md}
`CLAUDE.md` is a text file, written in Markdown, that lists your project's conventions and rules for the Claude Code agent. The agent reads it at the start of each session. Write it once, upfront, and update it when the rules change, instead of repeating the same instructions in every chat.

Good content is short and concrete: how to run the tests, which folders matter, naming rules, and things never to do ("never edit the generated files"). Vague advice such as "write clean code" adds little. If an agent keeps making the same mistake, add a line to the file.

## CLAUDE {#claude}
People often say just "CLAUDE" as a short name for that file, as in "put it in CLAUDE". It is the same file. Other tools use their own names, so check which file your agent actually reads.

## AGENTS.md {#agents-md}
`AGENTS.md` is a similar Markdown file meant to work with many different coding agents, not only one. It gives the same kind of help: build commands, code style and project rules. If you use more than one tool, one shared file avoids keeping several copies in step.

## README.md {#readme-md}
`README.md` is the Markdown file at the top of a project that tells people what it is and how to use it. It is written for humans first: what the project does, how to install it, a short example.

An agent reads it too, so it is useful background. Keep the instructions for humans in the README and the rules for agents in the agent file. Mixing them makes both harder to read.

## README {#readme}
"README" without the extension means the same thing. Many older projects use plain `README` or `README.txt`. The name is written in capitals so that it appears first in a folder listing.

## LICENSE {#license}
A `LICENSE` file states the legal terms under which others may use, copy and change your code. Without one, the default in most countries is that nobody else has any right to reuse it. Common choices are MIT and Apache 2.0, which are permissive, and the GPL, which requires that changes be shared under the same terms.

If an agent writes code for you, you remain the owner of the project and the one who chooses the license.

## A worked example {#example}
A small `CLAUDE.md` for a web project could look like this:

```markdown
# Project rules

- Run the tests with `npm test` before saying a task is done.
- Source code is in `src/`. Never edit files in `dist/`; they are generated.
- Use single quotes and two-space indentation.
- Do not add new dependencies without asking.
```

Check the file against four questions:

1. Does it say how to verify work? Yes, the test command.
2. Does it name no-go areas? Yes, `dist/`.
3. Does it set a style? Yes, quotes and indentation.
4. Does it limit risky actions? Yes, no new dependencies.

Four short lines already prevent the most common surprises. The README for the same project would instead describe what the app does and how to install it.

## A common mistake {#mistake}
Writing a very long rules file. Long files are skipped or half-remembered, and they go out of date. Keep it short, and add a rule only when a mistake has happened twice. A second mistake is leaving secrets such as passwords in any of these files, since they usually end up in a public repo.

## Key points {#key-points}
- A repo holds the project and its history, and it is all the agent can see.
- `CLAUDE.md` and `AGENTS.md` carry rules for agents. `README.md` explains the project to people.
- A `LICENSE` file says how others may reuse the code.
- Keep the rules short and concrete, and never put secrets in these files.
