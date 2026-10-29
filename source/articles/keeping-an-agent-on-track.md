# Keeping an agent on track

**Covers:** Prompt, Prompting, Scope creep, Losing the thread

## A fast, literal helper {#overview}
Think of an agent as a very fast assistant who takes you at your word. That is its strength, and also its risk. If your instructions are vague, it fills the gaps with guesses. If they are broad, it may do more than you wanted. And in a long conversation, it may quietly stop following rules you set at the start. Let's look at how to write instructions that work, and at the two ways a session tends to drift.

## Prompt {#prompt}
A prompt is what you tell the agent, written in plain language. In vibecoding it does the job that code does in ordinary programming: it is how you say what should happen. A good one has four parts: a goal, the context the agent needs, the limits it must respect, and a way to tell when the job is done.

Compare "make the login better" with this: "On the login page, show an error message under the password box when sign-in fails. Change only `login.js` and its test. The test should check that the message appears." The second gives the agent something to aim at, and gives you something to check it against.

## Prompting {#prompting}
Prompting is the craft of writing those instructions so that you get what you meant. Like any craft, you get better with practice, and a few habits help almost every time:

- Say the outcome you want, not only the activity.
- Show an example of the pattern instead of describing it at length.
- Break a big job into small steps you can check one at a time.
- Ask for a plan before any code, so a wrong approach is cheap to fix.
- Say what must not change.

When something goes wrong, improve the instruction and try again. And when a prompt works well, save it. One success then becomes a playbook you can reuse.

## Scope creep {#scope-creep}
Sometimes you ask for one thing and the agent does that thing plus a few more: it changes extra files, adds a feature, tidies code you did not mention. This is called scope creep. The agent usually means well, but a bigger change is harder for you to review, and mistakes hide in the extra lines.

You can prevent it in the prompt by naming the files and saying "only". You can catch it in review by comparing the list of changed files with what you asked for. If extra changes appear, ask the agent to undo them and keep the task small.

## Losing the thread {#losing-the-thread}
Here is something that surprises many people. In a long session, the agent can start to forget or ignore the rules and decisions you gave it earlier. The conversation has a limited memory, and old instructions fade as new text pushes them out. We call this losing the thread.

You will notice it when the agent repeats a mistake you already corrected, forgets a naming rule, or contradicts an earlier decision. The fixes are simple. Restate the key rules, put the lasting ones in the project's rules file, and when a session gets long, start a new one with a short summary of where you stand.

## A worked example {#example}
Say you ask, "Add a dark mode." When the agent finishes, you check the changes.

| Check | What you find | What to do |
|---|---|---|
| Files changed | 11 files, though dark mode needs about 3 | Scope creep: ask why |
| Extra edits | The agent also renamed several variables | Ask it to undo the renames |
| Later in the session | It uses double quotes again after you asked for single quotes | Losing the thread: restate the rule |

A better first instruction would have been: "Add a dark mode toggle. Change only `theme.js`, `App.js` and `styles.css`. Use single quotes. Do not rename anything. Show a plan first."

See what that prompt does? It names the files, limits the changes, repeats the style rule and asks for a plan. It takes 20 seconds to write and saves a long review.

## A common mistake {#mistake}
A common slip is trying to rescue a drifting session by arguing with the agent for another hour. A long, confused chat only makes things worse. Stop, write the current state and the rules in a few lines, and begin a new session. Another slip is writing a very long prompt full of small rules. A short, clear one with an example works better.

## Key points {#key-points}
- A prompt states the goal, the context, the limits and how to check the result.
- Good prompting is specific, uses examples, breaks work into steps and asks for a plan first.
- Scope creep means the agent did more than you asked. Name the files and say "only".
- In a long session the agent can lose the thread. Restate the rules, or start fresh with a summary.
