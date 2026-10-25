# Web application security

[Home](../README.md#challenge-categories) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Identify the boundary that explains the observed behavior: request parsing, authentication, authorization, template evaluation or database access. A useful question ties one boundary to the actual request and the relevant source.

The examples below are suggested wording. They have not been tested as live Overview triggers, and appearance is not guaranteed. The concrete scenarios are illustrative; replace their facts with your own evidence.

## What to include

| Keep | Why it matters |
| --- | --- |
| Framework and relevant version | Rendering, session and parser behavior can depend on the implementation. |
| Request method, path and relevant parameter | Different routes or methods can reach different checks. |
| Verified identity and role | A cookie's presence or a 200 response alone does not establish either. |
| Exact predicate or short source excerpt | It identifies the condition the request must satisfy. |
| Response difference after one controlled change | It helps distinguish competing explanations. |

Use a minimal source excerpt that preserves the decision being investigated. Omit unrelated route code and investigation history. Keep accurate names such as SQL injection, authorization and template evaluation; replacing them with vague terms can change the question.

## Try this question

A general question can establish the concept:

```text
How does authentication differ from authorization in a Flask application?
```

Then supply the evidence needed to explain a specific result:

```text
Why does my local Flask CTF app return 403 for GET /admin? Server-side inspection confirms the session has user_id=7 and role="user". GET /profile returns that user's details. The admin handler requires session["role"]=="admin". Explain the authorization decision and what source locations I should inspect to find where the role is created or updated. Separate confirmed behavior from vulnerability hypotheses.
```

Here, the supplied role does not satisfy the supplied predicate. That explains the decision in this scenario; it does not establish a way to change the role.

### Template evaluation

For rendering questions, retain the call that consumes the input and the corresponding template. This illustrative question narrows the boundary:

```text
In a local Flask CTF app, the route calls render_template("page.html", value=request.args["name"]). The template contains {{ value }}. With name={{7*7}}, the response contains literal {{7*7}}. Which stage treats the input as data rather than template source, and what source change would explain different behavior?
```

Do not assume template evaluation implies a sandbox escape. If a Jinja sandbox is present, identify its configuration: the [Jinja documentation](https://jinja.palletsprojects.com/en/stable/sandbox/) describes restrictions on private and internal attribute access by default.

## If that does not help

If the [Overview disappears after editing](troubleshooting.md#disappeared-after-editing), retain the current request, verified state and decisive predicate in one complete query. Remove resolved questions rather than appending contradictory history.

If the role is now verified as `admin` but the response remains 403, the question has changed. State the new observation and ask which remaining check or request-processing layer produces the response. If the answer ignores the predicate, ask it to evaluate that predicate using the supplied role; see [answers that ignore data](troubleshooting.md#answer-ignores-data).

## Check the answer

Trace the relevant value from its creation to the check that consumes it. Confirm which application or intermediary returned the status. For template questions, distinguish input displayed in a response from input evaluated as template syntax. Compare any proposed explanation with the exact source and controlled observations available under the event rules.

The [source notes](sources.md) distinguish reconstructed research observations from these suggested queries. No application instance was executed for this page.

## Related pages

Use [network forensics](network-forensics.md) for HTTP framing and capture exports, [reverse engineering](reverse-engineering.md) for program checks, and [query updates](search-patterns.md#add-or-rewrite) when a solved question leads to a new failure.
