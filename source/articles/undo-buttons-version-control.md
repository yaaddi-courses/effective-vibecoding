# Version control as an undo button

**Covers:** Version control, Branch, Commit, Force-push, Force push

## Why you want an undo for the whole session {#overview}
An agent can change dozens of files in one request. If you do not like the result, undoing it by hand is slow, and if you have already built more on top of it, it is nearly impossible. Version control gives you a reliable undo for the entire project, and a few habits make it work well with an agent.

## Version control {#version-control}
Version control is a system, most often Git, that records every change to your project over time. You can see what changed, who changed it and why, and you can return to any earlier state. It turns a risky experiment into a safe one, because going back costs seconds.

Use it before you start. A clean starting point, with everything saved, means that after a session you can always tell exactly what the agent changed.

## Branch {#branch}
A branch is a separate line of work inside the same project, where you can try changes without touching the main version. If the experiment fails, you throw the branch away. If it works, you merge it back.

For agent sessions, ask the agent to work on its own branch. The main line stays safe, and reviewing becomes easy: everything that differs from the main version is the agent's work.

## Commit {#commit}
A commit is a saved snapshot of your project with a short message describing the change. Each commit is a point you can return to.

Commit in small steps: after each working change, not at the end of the day. Each commit is an undo point, and small ones are easy to review and easy to reverse. Write messages that say what changed and why, such as "Add city lookup, handle unknown city".

## Force-push {#force-push}
A force-push is a push that overwrites the shared copy of a branch with your local version, discarding whatever commits were there before. A normal push is refused if it would lose someone's work. A force push skips that safety check.

It has legitimate uses, but it is dangerous on a branch other people use, because their work can vanish. Never let an agent do it without your explicit approval. If you must, the safer form is `--force-with-lease`, which refuses when someone else has pushed in the meantime.

## Force push {#force-push-spaced}
You will also see the spelling without the hyphen. It means the same thing and carries the same risk. Treat any request to "force" a push as an action to stop and think about.

## A worked example {#example}
A safe routine for one agent session:

```bash
git switch main
git status                    # confirm nothing is unsaved
git switch -c agent/add-search
# ... agent works; after each working step:
git add -A
git commit -m "Add search box"
# ... review the changes, run the tests
git diff main
```

Now compare two endings:

1. **It went well.** You review `git diff main`, run the tests and merge the branch. The history shows each small step.
2. **It went badly.** The agent broke the layout in the third step. You return to the second commit with `git reset --hard HEAD~1` and lose only one step. If you have not committed, you delete the branch and begin again with nothing lost on main.

Without version control, the second ending means trying to remember what the agent changed. With it, the undo takes a few seconds.

## A common mistake {#mistake}
Letting an agent accumulate one huge uncommitted change. If it is wrong, you can only accept all of it or none of it. Commit often to keep your options open. A second mistake is running commands such as `git reset --hard` or a force push without reading what they do, just because an agent suggested them.

## Key points {#key-points}
- Version control records every change and lets you go back to any earlier state.
- Do agent work on a branch so the main version stays safe.
- Commit after each small working step. Each commit is an undo point.
- A force push can destroy other people's work, so never allow it without approval.
