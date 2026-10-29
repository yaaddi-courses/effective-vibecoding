# Checking what an agent produces

**Covers:** Diff, Hallucination

## A strong first draft, never a final answer {#overview}
An agent writes code quickly and usually plausibly. Because it looks finished, it is tempting to accept it. But plausible is different from correct. Two habits close the gap: reading exactly what changed, and spotting claims that the agent invented. Both take minutes and prevent most of the costly surprises.

## Diff {#diff}
A diff is the exact list of changes between two versions of your files: which lines were added, which were removed and which were edited. When an agent finishes a task, the diff is the real answer to "what did it do?" It is more reliable than the agent's own summary, which may leave things out.

Read a diff the way a reviewer would. Look first at the list of changed files: is it what you expected, or did the agent touch extra ones? Then read each change. Lines starting with a minus sign were removed, and lines starting with a plus sign were added. Ask of each change: is it needed for the task, is it correct, and does it follow our conventions? Pay special attention to deleted code and to changed tests, since weakened tests are a common way for something to "pass".

## Hallucination {#hallucination}
A hallucination is a confident statement by an AI model that is false, such as a function, a command-line option or a fact that does not exist. The model is not lying. It predicts text that looks right, and sometimes that text points to something that was never there.

Typical examples in code: a method name that sounds natural but is not in the library, an option for a command that was never added, a version number that is wrong, or a reference to a file that is not in your project. The tone gives no clue, because it sounds exactly as sure as a correct answer.

The defence is to check anything you cannot already verify. Run the code, look in the official documentation, or ask the tool itself for its help text. If a call fails with "no such attribute", suspect a hallucination before you suspect your own setup.

## A worked example {#example}
An agent adds a call to read a web service's reply. The diff shows these changes:

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

Review it in order:

1. Files changed: two. The task only mentioned the weather code, so ask why a test changed.
2. The line `response.get_json()` looks natural, but this library's response object has `json()`, not `get_json()`. That is a hallucinated method, and running the code would raise an error.
3. The test used to check that the result was 21. Now it only checks that something came back. The agent weakened the test, probably to make it pass.
4. Decision: ask the agent to fix the method name, restore the original assertion, and explain why it changed the test.

All three problems were visible in the diff before anything was run.

## A common mistake {#mistake}
Reading only the agent's summary. A summary says what the agent intended, and the diff says what it did. Another mistake is trusting code because it compiles or "looks right". Only running it, with a realistic test, shows that it works.

## Key points {#key-points}
- A diff shows exactly what changed. Read it as a reviewer, and ask why each file was touched.
- A hallucination is a confident invention, such as a method or option that does not exist.
- Verify anything you cannot already confirm by running it or checking the documentation.
- Watch for weakened tests and unexplained deletions.
