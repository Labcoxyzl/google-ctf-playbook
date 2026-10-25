# Search patterns

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Challenge categories](../README.md#challenge-categories) · [Sources and evidence](sources.md)

Write the question you need answered now, with sufficient evidence. These patterns cannot guarantee an Overview.

## Current question

Use the normal top Search box and make each query understandable on its own. Google's [search tips](https://support.google.com/websearch/answer/134479?hl=en) recommend starting simply, adding descriptive words as needed and choosing terms likely to appear in relevant material.

A useful query contains the problem, necessary environment and data, latest relevant observation, and one requested result. These labels are optional:

```text
How or why [one current technical question]?
The relevant environment is [artifact, platform and version where needed].
The confirmed facts are [exact values and the smallest sufficient example].
The latest relevant test was [action], which produced [observation].
Give [one bounded result] and [a way to check it].
```

“The smallest sufficient example” must still contain every dependency of the requested answer. If you ask for recovered bytes, supply the target bytes and exact transformation. If you ask for a method, say which values are known and which are missing.

For example, this proposed query supplies a complete toy calculation:

```text
How do I recover four unsigned bytes when target=[0,255,1,2] in decimal and target[i]=((input[i]^0x5a)+i)&255 for i=0..3? Give the recovered bytes in hexadecimal and verify them with the forward transformation.
```

The locally checked answer is `5a a4 a5 a5`; Google response behavior is untested. See [reverse engineering](reverse-engineering.md) for types and input details.

## Add or rewrite

Add a fact when the question is still the same. Rewrite when the task, assumptions or relevant evidence have changed. The handoffs do not establish that either style produces Overview more often.

| Situation | What to do |
| --- | --- |
| Same inverse, newly recovered target array | Add the named array, its numeric base and indexing. |
| An observation contradicts an assumption | Remove the assumption and state the observation. |
| An earlier step is solved | Keep its verified result; ask about the remaining failure. |
| Two explanations remain plausible | State both and request an observation that distinguishes them. |

Suppose the toy calculation above succeeds, but the program rejects what you type. Appending “still fails” does not explain the new problem. Rewrite around the input representation:

```text
A program reads four raw bytes without hex decoding and checks target[i]=((input[i]^0x5a)+i)&255 for i=0..3 against decimal target=[0,255,1,2]. I verified that raw bytes 5a a4 a5 a5 satisfy the check, but I typed the text 5aa4a5a5. Which four bytes does the reader receive, and why does the check fail?
```

The first four text bytes are hexadecimal `35 61 61 34`. The arithmetic and the input representation are separate checks. This example assumes the raw input routine stated in the question; inspect the actual program before carrying that assumption over.

Do not depend on a prior Overview to supply omitted context. The documented mobile follow-up flow [enters conversational mode](https://blog.google/products-and-platforms/products/search/ai-mode-ai-overviews-updates/). For this guide's ordinary-Search workflow, put the complete current question back in the top Search box. If the Overview disappears, use [disappeared after editing](troubleshooting.md#disappeared-after-editing).

## Operators

Use operators when you need a specific source, phrase or document type. Google documents them as retrieval refinements in its [search refinement guide](https://support.google.com/websearch/answer/2466433?hl=en).

| Operator | Example | What it changes |
| --- | --- | --- |
| Exact phrase | `"stack smashing detected" meaning` | Searches for the quoted wording. |
| Site restriction | `site:docs.python.org gzip EOFError` | Limits retrieval to the named site. |
| Exclusion | `jaguar speed -car` | Excludes the unwanted word to reduce ambiguity. |
| File type | `ELF specification filetype:pdf` | Requests a particular document format. |
| Date range | `protocol specification after:2024-01-01 before:2026-01-01` | Narrows by Google's document-date handling. |

Keep the operator attached to its value: `site:docs.python.org`, not `site: docs.python.org`. A date restriction is not proof of a document's version.

These controls do not establish an Overview forcing method. If an old restriction no longer helps the current question, remove it. Do not quote an entire investigation narrative just because one exact error message matters. Under an Overview-only rule, locating a document does not automatically permit opening it; check [rules and surfaces](troubleshooting.md#rules-and-surfaces).

## Terminology

Keep the accurate technical name and explain the observed mechanism. Expanding an abbreviation can clarify a question; replacing it with a euphemism can remove the distinction you need. No lexical bypass is established by the evidence.

| Term or distinction | Context that makes the question useful |
| --- | --- |
| XOR, rotation, signedness | Width, operation order, casts and constants in the original expression. |
| RSA public exponent, ECDSA nonce | Exact construction and relationships; a nonce is not a signing key. |
| Authentication and authorization | Established identity, required role and the actual access predicate. |
| HTTP framing and compression | Export format, transfer framing and content encoding. |
| Stack canary and return address | Which saved value changed and where the program failed. |
| Least-significant-bit extraction | Channel order, bit plane, traversal and byte packing. |

When uncertain, preserve the ambiguity explicitly: “the decompiler displays a signed value; I have not confirmed the original type.” Ask which check would resolve it. Use the [category guide](../README.md#challenge-categories) for the facts specific to your artifact.

## Large inputs

There is no established best word count or modern Overview cutoff in the supplied evidence. A longer historical query produced a response, but that does not prove every detail was used. A short query can also omit the only value needed to solve the problem.

Keep the full investigation record locally. In Search, retain exact constants, complete required arrays, byte widths, state updates, framing and the observation that changed your hypothesis. Remove the diary of opening tools, abandoned guesses and already resolved questions.

Split a long investigation at a real dependency boundary. Ask about one transformation or protocol layer, check the result using permitted methods, then carry the verified output into the next complete query. If an exact answer requires the whole dataset, do not silently replace it with a prefix. Either include the required data or ask a method question and state that the sample is partial.

When an answer overlooks data, request a check using that data. Continue with [answer ignores data](troubleshooting.md#answer-ignores-data) or [sources and evidence](sources.md).
