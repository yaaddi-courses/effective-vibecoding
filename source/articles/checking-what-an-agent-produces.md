# Checking what an agent produces

**Covers:** Diff, Hallucination

## A strong first draft, never a final answer {#overview}
When an agent hands back its work, it looks finished, and that is exactly the trap. The code reads well, the explanation sounds sure of itself, and it is tempting to say "great, thanks" and move on. But plausible and correct are two different things. In this article, you will learn two habits that close the gap: reading exactly what changed, and spotting things the agent made up. Both take a few minutes, and between them they prevent most of the expensive surprises.

## Diff {#diff}
Let's start with a question you should always ask when an agent finishes: "What did you actually do?" The best answer is not the agent's own summary, it is the diff. A diff is the exact list of differences between two versions of your files: which lines were added, which were removed and which were edited. The summary tells you what the agent meant to do. The diff tells you what happened, and it cannot leave anything out.

Read it the way a reviewer would. First look at the list of changed files and ask, is this what I expected, or did something extra get touched? Then go through the changes one by one. A line that starts with a minus sign was removed, and a line that starts with a plus sign was added. For each change, ask three things: is it needed for this task, is it correct, and does it follow our conventions? Give extra attention to deleted code and to changed tests. A weakened test is one of the easiest ways to make a broken change look like it passes.

## Hallucination {#hallucination}
Now the second habit. Sometimes an AI model states something with complete confidence that is not true: a function that does not exist, a command-line option nobody ever added, a made-up fact. That is called a hallucination. The model is not lying to you. It predicts text that looks right, and now and then the text points at something that was never there.

In code, you will meet it as a method name that sounds perfectly natural but is not in the library, a wrong version number, or a reference to a file your project does not have. Here is the part that catches people out: the tone gives no clue. A hallucinated answer sounds exactly as sure as a correct one.

So the defense is simple. Check anything you cannot already verify. Run the code, look in the official documentation, or ask the tool for its help text. And when a call fails with "no such attribute", suspect a hallucination before you suspect your own setup.

## A worked example {#example}
Let's go through a real-looking case together. An agent adds code to read a web service's reply, and the diff shows this:

```text
 src/weather.py
-    data = fetch(city)
+    response = requests.get(URL, params={"city": city})
+    data = response.get_json()
+    return data["temp"]

 tests/test_weather.py
-    assert result == 21
+    assert result is not None
```

We review it in order.

1. Two files changed. You only mentioned the weather code, so the first question is: why did a test change?
2. The line `response.get_json()` looks natural, but this library's response object has `json()`, not `get_json()`. That is a hallucinated method, and running the code would raise an error.
3. Look at the test. It used to check that the result was 21. Now it only checks that something came back. The agent weakened the test, most likely to make it pass.
4. Our decision: ask the agent to fix the method name, restore the original assertion, and explain why it touched the test.

Notice that all three problems were visible in the diff before anything was run. That is the value of reading it.

## A common mistake {#mistake}
A common slip is to read only the agent's summary. The summary says what the agent intended, and the diff says what it did. Another is to trust code because it compiles or "looks right". Only running it with a realistic test shows that it works.

## Key points {#key-points}
- A diff shows exactly what changed. Read it as a reviewer, and ask why each file was touched.
- A hallucination is a confident invention, such as a method or option that does not exist.
- Verify anything you cannot already confirm, by running it or checking the documentation.
- Watch for weakened tests and unexplained deletions.
