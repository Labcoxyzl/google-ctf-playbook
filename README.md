# Google CTF Playbook

A manual reference for CTFs that permit only the **Overview that appears automatically in ordinary Google Search**. Use it to improve your next search, recover from an unhelpful revision, and check the answer against challenge evidence.

This repository contains Markdown reference pages. Google decides when to show an Overview; no wording guarantees one. [Google's feature help](https://support.google.com/websearch/answer/14901683?co=GENIE.Platform%3DDesktop&hl=en) describes that conditional behavior.

## Find the next useful edit

| What is happening? | Start here |
| --- | --- |
| I keep searching, but no Overview appears. | [No Overview](#no-overview) |
| It disappeared after I added more context. | [Disappeared after editing](#disappeared-after-editing) |
| It appears, but ignores my values or newest observation. | [Answer ignores data](#answer-ignores-data) |
| I need a better question for this challenge. | [Challenge categories](#challenge-categories) |
| I am unsure whether a button or search surface is allowed. | [Stay within the rules](#stay-within-the-rules) |

## No Overview

Check that you are using ordinary Search with **All** selected. The **Web** filter deliberately removes Overviews. A generating message, a collapsed answer, an offer to generate, and a traffic block need different responses; use the [result-state guide](docs/troubleshooting.md). [Google's feature help](https://support.google.com/websearch/answer/14901683?co=GENIE.Platform%3DDesktop&hl=en) explains the filter and current availability.

Turn a loose topic into one answerable technical question. For example, replace `gzip pcap broken` with:

```text
Why does gzip decompression report an unexpected end of file after I export an HTTP/1.1 response from Wireshark? What observations distinguish an incomplete export from incorrect message boundaries?
```

Use the error you actually observed. Keep decisive facts, remove irrelevant history, and relax search restrictions that no longer serve a purpose. This is a practical reformulation, not a tested trigger. Continue with [missing-Overview recovery](docs/troubleshooting.md#no-overview) or your [category](#challenge-categories).

## Disappeared after editing

Start from the last useful wording, then decide whether the new fact changes the question. If you are still solving the same problem, add the fact with its name and units. If you have solved one step or disproved an assumption, rewrite around the current problem and retain the verified result.

For example, after calculating input bytes, “the checker rejects what I typed” is an input-representation question. Carry the bytes, input routine and observed rejection into a complete new search. The [reverse-engineering example](docs/reverse-engineering.md) shows this transition.

Submit the complete revision in the normal top Search box. Do not rely on `it still fails` to carry the previous context. The earlier Overview may not return even with the old wording. See [add or rewrite](docs/search-patterns.md#add-or-rewrite) and [disappearance recovery](docs/troubleshooting.md#disappeared-after-editing).

## Answer ignores data

Ask for an intermediate result or a check that depends on your exact facts. For a byte checker, request the recovered bytes **and** the output of the original forward expression. For a crypto problem, ask which candidates satisfy the supplied bounds and original equation.

Repeating your values in the answer is not enough. Check whether the reasoning uses them correctly, using the challenge evidence and tools the event permits. If a necessary value is unknown, request the remaining cases and the observation that would distinguish them. See [ignored-data recovery](docs/troubleshooting.md#answer-ignores-data).

## Query recipe

```text
Why does [technical object] show [observed behavior]?
Confirmed: [the decisive facts and exact values].
The latest relevant test was [action], which produced [result].
Explain [one current question] and give [a concrete check].
```

The labels are optional. Preserve widths, signs, indexing, state relationships and data representation when they change the answer. Remove resolved questions and irrelevant diary entries. There is no established ideal word count. Use [search patterns](docs/search-patterns.md) for worked revisions, large inputs, terminology and search operators.

## Challenge categories

| Challenge | Useful question to frame | Open the guide |
| --- | --- | --- |
| Reverse engineering | Which operation, type or input representation explains the mismatch? | [Checkers and byte transformations](docs/reverse-engineering.md) |
| Cryptography | Which method's assumptions match these parameters and samples? | [RSA, nonces and mathematical constraints](docs/cryptography.md) |
| Pwn and OS internals | What does this crash or memory observation actually establish? | [Corruption, mitigations and system behavior](docs/pwn-os.md) |
| Web | Which parsing, authentication or authorization step explains this response? | [Requests, sessions and rendering](docs/web.md) |
| Network forensics | Which framing or decoding layer is incomplete or misinterpreted? | [Streams, HTTP and compressed data](docs/network-forensics.md) |
| Disk and memory forensics | Which correlated artifact distinguishes the competing explanations? | [Timelines, process identity and plugin output](docs/disk-memory-forensics.md) |
| OSINT | What public-scene observation could rule out this candidate? | [Location clues and uncertain readings](docs/osint.md) |
| Steganography and miscellaneous decoding | Which extraction or representation assumption fails a structural check? | [Bit extraction and decoding chains](docs/stego-misc.md) |

## Stay within the rules

This guide assumes ordinary text Search and an automatically displayed Overview. An **Ask anything** follow-up can move into a separate conversational experience: Google explicitly documents that transition on mobile. Use the normal Search box for another self-contained question, and check the actual surface before continuing. [Google's January 2026 announcement](https://blog.google/products-and-platforms/products/search/ai-mode-ai-overviews-updates/) describes the transition.

Expanding **Show more**, pressing **Generate**, uploading an image through Lens, or opening a cited webpage are distinct actions. Do not assume they are permitted because the initial Overview is permitted. If the event allows only the visible automatic answer, work within that limit. The references in this repository support preparation; they do not grant permission to open external pages during a challenge. See [rules and search surfaces](docs/troubleshooting.md#rules-and-surfaces).
