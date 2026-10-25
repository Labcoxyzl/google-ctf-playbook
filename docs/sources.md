# Sources and evidence

[Playbook home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

The practical advice in this playbook combines the supplied ChatGPT handoff, the secondary Gemini handoff and current Google documentation. The primary handoff supplies the main workflow and category examples. The secondary handoff contributes useful technical vocabulary and question forms, with unsupported trigger claims removed.

Product sources were reviewed on **26 October 2026**. The suggested search questions are editing aids. Their wording does not promise an Overview or a correct answer.

## What was reviewed

| Input | Coverage | What the review established |
| --- | --- | --- |
| ChatGPT handoff | All 34 files: Markdown, structured records, source registry, C fixture, image and validation scripts | The core workflow, reconstructed observations, proposed templates, technical examples and explicit evidence gaps |
| Gemini handoff | All 53 files: report exports, structured libraries, raw source extracts, telemetry, scripts and charts | Useful vocabulary and question patterns, duplicated evidence, export discrepancies and claims that exceed their support |
| Current Google sources | Eleven relevant Help, developer, product-paper and announcement extracts | Product boundaries, conditional appearance, query refinement, follow-up behavior and current availability guidance |
| Patent attribution records | Metadata and opening excerpts for the two disputed records | The named assignees; no conclusion about production implementation |

The original archives and extracted files are retained outside this public repository. Their fingerprints identify the reviewed inputs without publishing scripts, charts or source-page copies here.

| Archive | SHA-256 |
| --- | --- |
| Primary ChatGPT handoff | `ae23789ba94607b7d103db30d0a91289815c17065f39d45c5bbc476d49bea0c7` |
| Secondary Gemini handoff | `7e201bf7da850c16e942a619ad0e5591b379189f579ba9ef830412899669ea14` |

The Gemini report's Markdown, HTML and 20-page PDF were compared. Most text agrees, but the PDF clips a long token example and the other exports contain broken relative chart links. Its 36 raw extract files represent nine distinct browsed pages and six search batches, often repeated in multiple export formats. Repeated exports do not provide independent corroboration.

## What the evidence supports

| Evidence class | What it supports | What it cannot establish |
| --- | --- | --- |
| Current official documentation | Behavior described for the stated product, surface and rollout | A guarantee for an individual query or every account interface |
| Reconstructed historical observations | That the handoff reports a particular result in its recorded environment | A reproducible success rate, complete transcript or controlled causal comparison |
| Local technical checks | The arithmetic or format behavior of a supplied synthetic example | Whether its wording will make Google display an Overview |
| Suggested query patterns | A practical way to express the current question and necessary facts | A privileged instruction format, optimal length or reliable triggering recipe |
| Third-party studies and architecture explanations | Background hypotheses and source leads, within their methods | Undocumented Google thresholds or an individual contestant's probability of success |

The primary handoff records **17 text submissions**: 15 completed Overview observations, one pending result and one traffic block. There are 16 distinct query strings because one was repeated. These are selected exploratory observations, not a 15-out-of-17 success benchmark. The pending and blocked states are not measured negative outcomes.

The reported environment was signed out, English, desktop cloud Chrome with US Google context. Original result screenshots, full response captures, raw browser snapshots and network traces did not survive. The surviving image is the synthetic input fixture. Response notes therefore support qualified historical observations, not independently replayable results.

All **27 proposed query templates** in the primary handoff were untested as written. Related observed queries do not make a new template tested. The planned comparison of adding context versus rewriting was interrupted before it produced a result. The guidance in [search patterns](search-patterns.md#add-or-rewrite) is a reasoned workflow recommendation.

Two separate visual-search states reportedly produced Overviews. They used Lens-specific surfaces, and both response notes contain technical errors. They do not establish multi-image support, compliance with ordinary text-search rules, or better answer quality.

## Locally checked examples

The primary handoff's three validation scripts were inspected and executed unchanged. They passed package integrity checks, technical example checks and a structural token decode. These checks ran locally and did not submit searches to Google.

| Example or check | Verified result | Where it helps |
| --- | --- | --- |
| Unsigned-byte inverse | 65,536 byte/index round trips; the original target recovers `ABCD` | [Reverse engineering](reverse-engineering.md) |
| Wraparound and representation | Target `[0,255,1,2]` recovers raw hex `5a a4 a5 a5`; typing `5aa4a5a5` supplies different bytes | [Reverse engineering](reverse-engineering.md) |
| Bounded toy RSA | For `e=3`, `n=11413`, `c=5610`, `0 <= m < 64`, the unique candidate is `m=42` | [Cryptography](cryptography.md) |
| Synthetic chunked and gzip data | Correct decoding order round-trips the fixture; deliberate truncation raises `EOFError` | [Network forensics](network-forensics.md) |
| Bundle manifest | All 33 manifest payload hashes match; the manifest itself makes 34 primary files | Input integrity only |
| Token bytes | Raw wire fields can be decoded from the provided sample | No field names, routing meaning or control mechanism established |

The gzip fixture is deliberately small; its decoder is not a general HTTP implementation. No real disk image, memory image or private challenge binary was analyzed. A correct result for one toy input does not validate every general explanation accompanying it.

## Claims not to rely on

| Tempting claim | Assessment and practical consequence |
| --- | --- |
| A fixed 9–14-word query reliably triggers an Overview | No such rule was established. Nineteen of the secondary handoff's twenty supposedly matching examples exceed fourteen whitespace-separated words. Preserve necessary facts instead of meeting a quota. |
| A percentage from a chart predicts the next query's outcome | The secondary trigger chart mixes studies and relabels categories. Observational prevalence is not the causal effect of rewriting a CTF question. No trigger percentages are used in the operational pages. |
| Replacing security terms defeats a known filter | No causal lexical bypass was established. Use accurate terms and explain the observed mechanism; do not change the meaning of the task. |
| Exact passage lengths, entity counts or a cosine threshold determine eligibility | The supplied sources do not establish deployed Google constants. These targets are excluded from query advice. |
| A delay reveals which hidden gate rejected the query | Timing alone cannot identify the internal cause. Diagnose the visible result state instead. |
| Hidden URL parameters, tokens or `folsrch` replay force the feature | No supported forcing method was found in the reviewed official sources. Structural decoding does not prove token semantics or make replay part of ordinary Search. |
| Patent diagrams describe the current search system | A patent describes claimed designs. It does not establish production behavior or a user-facing search trick. |
| A complete answer can be forced by saying “no follow-ups” | Missing values remain missing. Supply the necessary data or request conditional cases. |

For attribution, the [US20240256582A1 record](https://patents.google.com/patent/US20240256582A1/en) names Glean, and the [US12079185B2 record](https://patents.google.com/patent/US12079185B2/en) names Yext. Hosting on Google Patents does not make an invention Google's. Only the attribution metadata and opening excerpts were checked for this correction.

The secondary bundle also contains a query-optimizer script that fails syntax parsing. It was not repaired or included: the requested deliverable is a human reference, and its scoring rules are unsupported. Chart-generation code was inspected, while the existing images were reviewed directly. No chart is treated as an independently reproduced measurement.

## Sources and review date

These links support preparation and the claims stated here. During an event, external-page access remains subject to its rules. Descriptive link labels are shortened for readability; the original URLs identify the sources.

| Primary source | What it supports | Scope |
| --- | --- | --- |
| [Google Overview help](https://support.google.com/websearch/answer/14901683?co=GENIE.Platform%3DDesktop&hl=en) | Conditional appearance, mistakes, availability, Web filter behavior and documented follow-up transition | Maintained help; interface settings may change |
| [Google's January 2026 Search update](https://blog.google/products-and-platforms/products/search/ai-mode-ai-overviews-updates/) | Follow-ups from an Overview can enter the conversational experience | Announcement dated 27 January 2026; the described transition is mobile |
| [Conversational Search help](https://support.google.com/websearch/answer/16011537?co=GENIE.Platform%3DDesktop&hl=en) | The separate surface's follow-up and history behavior | Does not establish memory for a normal edited Search query |
| [Google search tips](https://support.google.com/websearch/answer/134479?hl=en) | Start simply, add useful descriptive terms and use recognizable vocabulary | General search guidance, not a trigger experiment |
| [Google search refinement](https://support.google.com/websearch/answer/2466433?hl=en) | Quotes, `site:`, exclusions, date operators, `filetype:` and filters | Retrieval controls, not guaranteed Overview controls |
| [Google Labs help](https://support.google.com/websearch/answer/13572151?hl=En&ref_topic=13544225) | Experiments and optional generation have separate behavior and eligibility | Do not import Labs requirements into core Search troubleshooting |
| [Google image-search help](https://support.google.com/websearch/answer/1325808) | Lens inputs and possible result types | Product capability does not establish event permission |
| [Google Search Central explanation](https://developers.google.com/search/docs/appearance/ai-features) | Conditional triggering and differences between search surfaces | Written for website owners; not a query optimization specification |
| [Google's March 2025 Search update](https://blog.google/products-and-platforms/products/search/ai-mode-search/) | Historical removal of a sign-in requirement in the announced rollout | Use current Help for present availability |
| [Google's May 2024 retrospective](https://blog.google/products-and-platforms/products/search/ai-overviews-update-may-2024/) | Historical issues with unusual queries, limited evidence and triggering restrictions | Historical explanation, not a current diagnostic formula |
| [Google's May 2025 product paper](https://search.google/pdf/google-about-AI-overviews-AI-Mode.pdf) | High-level design and conditional triggering | Product description, not a reproducible CTF benchmark |

All eleven sources were retrieved and reviewed as text extracts on 26 October 2026. Extraction may omit collapsed interface content or link targets; a saved extract is not a record of the user's actual account or browser. The current official sources support the product claims, while the handoffs support the qualified historical record.

## Limits and future checks

This publication did not run a fresh live Google experiment or inspect the competition's rulebook. It follows the user's stated restriction to the automatic Overview. Account, locale, language, device and rollout differences can affect the interface. Use the maintained help pages when checking eligibility before an event.

To evaluate your own permitted searches, retain the exact query, visible result state, relevant environment and a check of the answer. Compare appearance separately from whether the newest facts were used and whether the result was correct. A pending result or traffic block is missing measurement. A single success or disappearance does not explain Google's hidden mechanism.

Return to [the quick lookup](../README.md#find-the-next-useful-edit), [troubleshooting](troubleshooting.md), or [your challenge category](../README.md#challenge-categories).
