# Keeping an agent on track

**Covers:** Prompt, Prompting, Scope creep, Losing the thread

## A fast, literal helper {#overview}
An agent follows instructions closely and quickly. That is the strength and also the risk. If your instructions are vague, it fills the gaps with guesses. If they are broad, it may do more than you wanted. And if a conversation grows long, it may stop following rules you set at the start. This article covers the instructions you give and two ways a session can drift.

## Prompt {#prompt}
A prompt is the instruction you give the agent, written in plain language. In vibecoding it plays the role that code plays in ordinary programming: it is how you say what should happen. A good prompt has a goal, the context the agent needs, the limits it must respect, and a way to tell when the job is done.

Compare "make the login better" with "On the login page, show an error message under the password box when the sign-in fails. Change only `login.js` and its test. The test should check that the message appears." The second gives the agent something to aim at and something to be checked against.

## Prompting {#prompting}
Prompting is the craft of writing those instructions so that the result is what you wanted. It is a skill you improve by practice. Some habits help consistently:

- State the outcome you want, not only the activity.
- Give an example of the pattern you want instead of describing it at length.
- Break a large job into small steps that you can check one by one.
- Ask for a plan before any code, so that a wrong approach is cheap to fix.
- Say what must not change.

When something goes wrong, improve the instruction and try again. Saving a prompt that worked turns a single success into a reusable playbook.

## Scope creep {#scope-creep}
Scope creep is when an agent quietly does more than you asked, such as changing extra files, adding features or reformatting unrelated code. An eager agent often does this with good intentions, but the larger changeset is harder to review and hides mistakes.

Prevent it in the prompt by naming the files and saying "only". Catch it in review by comparing the list of changed files with your request. If extra changes appear, ask the agent to undo them and keep the task small.

## Losing the thread {#losing-the-thread}
Losing the thread is what happens in a long session when the agent begins to forget or ignore the rules and decisions you gave it earlier. The conversation has a limited memory, and old instructions fade as new text pushes them out.

Signs include the agent repeating a mistake you already corrected, forgetting a naming rule, or contradicting a decision. The fixes are simple: restate the key rules, put lasting ones in the project's rules file, and when a session gets long, start a new one with a short summary of where you stand.

## A worked example {#example}
You ask: "Add a dark mode." After the agent finishes, you check the diff.

| Check | What you find | Action |
|---|---|---|
| Files changed | 11 files, though dark mode needs about 3 | Scope creep: ask why |
| Extra edits | The agent also renamed several variables | Ask it to undo the renames |
| Later in the session | It uses double quotes again after you asked for single quotes | Losing the thread: restate the rule |

A better version of the first instruction would have been: "Add a dark mode toggle. Change only `theme.js`, `App.js` and `styles.css`. Use single quotes. Do not rename anything. Show a plan first."

That prompt names the files, limits the changes, repeats the style rule and asks for a plan. It takes 20 seconds to write and saves a long review.

## A common mistake {#mistake}
Fixing a drifting session by arguing with the agent for another hour. A long, confused chat makes the problem worse. Stop, write down the current state and the rules in a few lines, and begin a new session. A second mistake is writing a very long prompt full of small rules. A short, clear one with an example works better.

## Key points {#key-points}
- A prompt states the goal, the context, the limits and how to check the result.
- Good prompting is specific, uses examples, breaks work into steps and asks for a plan first.
- Scope creep means the agent did more than you asked. Name the files and say "only".
- In a long session the agent can lose the thread. Restate the rules or start fresh with a summary.
