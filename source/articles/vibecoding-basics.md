# What vibecoding is and where it helps

**Covers:** Vibecoding, AI, API, Boilerplate

## Directing instead of typing {#overview}
Programming used to mean writing every line yourself. Now there is another way: you describe what you want in plain language, and an assistant writes the code. You still decide what to build, and you still answer for the result. What changes is how your time is spent: less on typing, more on directing and checking.

In this article, we will look at the term itself, at the technology behind it, and at the kind of work where this style pays off most.

## Vibecoding {#vibecoding}
Vibecoding is building software by telling an AI coding agent what you want in everyday words, and then reviewing and steering what it produces. The word became popular in early 2025, after the researcher Andrej Karpathy described a style of working where you "give in to the vibes" and let the assistant write most of the code.

In practice there are two versions. The careless one accepts whatever the agent writes and moves on. That is fine for a throwaway experiment and falls apart on anything that matters. The disciplined one keeps you in charge: you set the goal, you read what changed, you run it, and you decide what to keep. This course teaches the second version.

## AI {#ai}
AI, short for artificial intelligence, is software that does tasks which normally need human judgment, such as understanding language, spotting patterns or writing text. The agents used in vibecoding are built on a large language model, a system trained on huge amounts of text and code to predict what comes next.

Two facts about such a model explain most of its behavior. First, it is very good at patterns it has seen often, which is why routine code usually comes out well. Second, it has no built-in sense of true and false, which is why it can say something wrong in a confident voice.

## API {#api}
An API, or application programming interface, is an agreed way for one program to ask another for something. A weather service, for example, may offer an API that returns tomorrow's forecast when you send it a city name.

APIs matter in vibecoding for two reasons. They are a place where an agent saves you real time, because it can read unfamiliar documentation and write the calls for you. They are also a place where it can mislead you, because it may invent a function that sounds right but does not exist. So always check a new call against the official documentation, or by running it.

## Boilerplate {#boilerplate}
Boilerplate is repetitive, predictable code that nearly every project needs: setting up folders, reading settings, wiring a standard form, adding the usual test scaffolding. It takes little creativity, but it takes time, and it is easy to get slightly wrong.

This is where agents shine. The pattern is common in their training data, the result is easy to check, and a mistake costs little. So hand the boilerplate to the agent, and keep your own attention for the parts that need judgment, such as what the product should actually do.

## A worked example {#example}
Say you want a small tool that shows the weather for a city. Let's see how the work divides.

| Step | Who does it best | Why |
|---|---|---|
| Decide what the tool should show | You | It is a product decision |
| Create the project folders, settings and a standard layout | The agent | Boilerplate |
| Write the calls to a weather API | The agent, then you verify | Saves reading the docs, but check the calls |
| Decide how to handle a city that is not found | You | It needs judgment about the user |
| Run the tool and try five cities | You | Only running it proves it works |

The agent might finish steps 2 and 3 in a few minutes. You then spend your time on steps 1, 4 and 5, and those are the ones that decide whether the tool is good.

## A common mistake {#mistake}
A common slip is to treat the agent's confidence as correctness. It sounds equally sure when it is right and when it is wrong. Another is to hand over the hard design decisions together with the boilerplate. Those are the tasks where a wrong answer is expensive, and a fast one does not help.

## Key points {#key-points}
- Vibecoding means directing an AI agent in plain language and reviewing its work, while you stay responsible for the result.
- AI models are strong on common patterns and can be confidently wrong.
- An API is a way for programs to ask each other for things. Check any call an agent writes for you.
- Boilerplate is the best work to hand to an agent. Keep judgment for yourself.
