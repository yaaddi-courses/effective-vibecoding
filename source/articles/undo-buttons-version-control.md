# Version control as an undo button

**Covers:** Version control, Branch, Commit, Force-push, Force push

## Why you want an undo for the whole session {#overview}
Imagine an agent changes thirty files in one request, and you do not like the result. Undoing that by hand is slow. And if you have already built more on top of it, it is nearly impossible. What you want is an undo button for the entire project, and that is exactly what version control gives you. In this article, we look at how it works and at a few habits that make it fit well with an agent.

## Version control {#version-control}
Version control is a system, most often Git, that records every change to your project over time. You can see what changed, who changed it and why, and you can return to any earlier state. It turns a risky experiment into a safe one, because going back costs seconds.

Use it before you start. A clean starting point, with everything saved, means that after a session you can always tell exactly what the agent changed.

## Branch {#branch}
A branch is a separate line of work inside the same project, where you can try changes without touching the main version. If the experiment fails, you throw the branch away. If it works, you merge it back.

For agent sessions, ask the agent to work on its own branch. The main line stays safe, and reviewing becomes easy: everything that differs from the main version is the agent's work.

## Commit {#commit}
A commit is a saved snapshot of your project with a short message describing the change. Each commit is a point you can return to.

So commit in small steps, after each working change, and not only at the end of the day. Small commits are easy to review and easy to reverse. Write messages that say what changed and why, such as "Add city lookup, handle unknown city".

## Force-push {#force-push}
A force-push overwrites the shared copy of a branch with your local version, and throws away whatever commits were there before. A normal push is refused when it would lose someone's work. A force push skips that safety check.

It has legitimate uses, but on a branch that other people use it is dangerous, because their work can vanish. So never let an agent do it without your explicit approval. If you must, use the safer form, `--force-with-lease`, which refuses when someone else has pushed in the meantime.

## Force push {#force-push-spaced}
You will also see the spelling without the hyphen. It means the same thing and carries the same risk. Whenever you see a request to "force" a push, treat it as a signal to stop and think.

## A worked example {#example}
Here is a safe routine for one agent session:

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

Now let's compare two endings.

1. **It went well.** You review `git diff main`, run the tests and merge the branch. The history shows each small step.
2. **It went badly.** The agent broke the layout in the third step. You go back to the second commit with `git reset --hard HEAD~1` and lose only one step. If you had not committed yet, you would delete the branch and start over, with nothing lost on main.

Without version control, the second ending means trying to remember what the agent changed. With it, the undo takes a few seconds.

## A common mistake {#mistake}
A common slip is letting the agent pile up one huge uncommitted change. If it turns out wrong, your only options are to accept all of it or none of it. Commit often to keep your options open. Another slip is running something like `git reset --hard` or a force push without reading what it does, just because an agent suggested it.

## Key points {#key-points}
- Version control records every change and lets you go back to any earlier state.
- Do agent work on a branch so the main version stays safe.
- Commit after each small working step. Each commit is an undo point.
- A force push can destroy other people's work, so never allow it without approval.
