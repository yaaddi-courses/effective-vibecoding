# The project files that tell an agent how to work

**Covers:** Repo, CLAUDE.md, CLAUDE, AGENTS.md, README.md, README, LICENSE

## A new colleague every morning {#overview}
Picture hiring a skilled colleague who forgets everything overnight. Every morning you would have to explain the project again: how you name things, which command runs the tests, what must never be touched. That is what an AI coding agent is like. It starts each session knowing nothing about your project. A human learns this over time, but an agent needs it written down. A handful of plain text files at the top of your project give it that background, and they help human readers too.

## Repo {#repo}
A repo, short for repository, is the folder that holds a whole project: its code, its settings and the complete history of changes, tracked by Git. Everything the agent needs to understand your project should live inside it, because that is all the agent can see.

A repo also gives you a safety net. If the agent makes a mess, you can compare against the saved history and go back.

## CLAUDE.md {#claude-md}
`CLAUDE.md` is a text file, written in Markdown, where you list the conventions and rules of your project for the Claude Code agent. The agent reads it at the start of every session. So you write your rules once, and update them when they change, instead of repeating the same instructions in every chat.

What goes in? Short, concrete things: how to run the tests, which folders matter, naming rules, and things never to do, such as "never edit the generated files". Vague advice like "write clean code" adds very little. And if the agent keeps making the same mistake, that is your cue to add a line to the file.

## CLAUDE {#claude}
You will often hear people say just "CLAUDE", as in "put it in CLAUDE". They mean the same file. Other tools use their own file names, so check which one your agent actually reads.

## AGENTS.md {#agents-md}
`AGENTS.md` is a similar Markdown file, but meant to work with many different coding agents instead of only one. It carries the same kind of help: build commands, code style and project rules. If you use more than one tool, a single shared file saves you from keeping several copies in step.

## README.md {#readme-md}
`README.md` is the Markdown file at the top of a project that tells people what it is and how to use it. It is written for humans first: what the project does, how to install it, and a short example.

An agent reads it too, so it is useful background. But keep the two jobs apart: put instructions for humans in the README and rules for agents in the agent file. Mixing them makes both harder to read.

## README {#readme}
"README" without the extension means the same thing. Many older projects use a plain `README` or `README.txt`. The name is written in capitals so that it shows up first in a folder listing.

## LICENSE {#license}
A `LICENSE` file states the legal terms under which others may use, copy and change your code. Here is the point many beginners miss: without one, the default in most countries is that nobody else has any right to reuse your code. Common choices are MIT and Apache 2.0, which are permissive, and the GPL, which requires that changes be shared under the same terms.

If an agent writes code for you, you still own the project, and you are the one who chooses the license.

## A worked example {#example}
Here is a small `CLAUDE.md` for a web project:

```markdown
# Project rules

- Run the tests with `npm test` before saying a task is done.
- Source code is in `src/`. Never edit files in `dist/`; they are generated.
- Use single quotes and two-space indentation.
- Do not add new dependencies without asking.
```

Let's test it with four questions.

1. Does it say how to verify work? Yes, the test command.
2. Does it name no-go areas? Yes, `dist/`.
3. Does it set a style? Yes, quotes and indentation.
4. Does it limit risky actions? Yes, no new dependencies.

Four short lines already prevent the most common surprises. The README of the same project would do a different job: describe what the app does and how to install it.

## A common mistake {#mistake}
A common slip is writing a very long rules file. Long files get skipped or half-remembered, and they go out of date. Keep it short, and add a rule only when a mistake has happened twice. Another slip is leaving secrets such as passwords in any of these files, since they usually end up in a public repo.

## Key points {#key-points}
- A repo holds the project and its history, and it is all the agent can see.
- `CLAUDE.md` and `AGENTS.md` carry rules for agents. `README.md` explains the project to people.
- A `LICENSE` file says how others may reuse the code.
- Keep the rules short and concrete, and never put secrets in these files.
