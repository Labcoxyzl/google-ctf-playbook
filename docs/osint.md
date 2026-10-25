# OSINT and public-scene clues

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Use the Overview to identify evidence that separates plausible candidates. A suggested country, street or landmark remains a hypothesis until it agrees with the challenge's actual scene and survives a meaningful conflicting observation.

## What to include

Record the public features you can actually see: readable sign text, road geometry, traffic direction, building arrangement and other distinctive objects. Separate exact transcription from uncertain OCR. Preserve accents and punctuation when readable; mark missing characters explicitly instead of silently completing a familiar name.

| Evidence | Useful description |
| --- | --- |
| Readable text | The sign clearly reads `Rua`; the remaining text is blurred. |
| Uncertain reading | A number may begin with `2`; this has not been confirmed. |
| Candidate locations | Portugal and Brazil remain possibilities; neither is established. |
| Matching features | Name the independent scene details that fit each candidate. |
| Conflicting features | Record an incompatible junction, sign or building arrangement. |
| Date and metadata | State a known image date or missing GPS information without inventing either. |

Broad clues such as language, roof color or traffic direction may fit several places. Ask for the observation that would separate them. See the [source notes](sources.md) for the distinction between proposed search wording and the handoff's reconstructed observations.

## Try this question

The examples are suggested wording. These exact searches have not been tested live and do not guarantee an Overview.

Start with a general discrimination question:

```text
Which public street-scene clues help distinguish Portugal from Brazil when the visible sign text is Portuguese?
```

Then include the actual uncertainty:

```text
Which observations would distinguish Portugal from Brazil in a public street-photo CTF? The sign clearly reads Rua, traffic keeps right and roofs have red tiles. EXIF GPS is absent. A blurred number may begin with 2, but that reading is uncertain. Neither country is confirmed. Which additional visible clues could rule out each candidate?
```

## If that does not help

If an answer confidently names a place from generic clues, ask it to expose the missing distinction. Replace the brackets with current observations:

```text
How can I test whether [public location candidate] matches this CTF scene? Confirmed features are [road geometry, sign text and building arrangement]. The candidate fits [independent matches] but conflicts with [specific observation]. The reading [text] remains uncertain. What observable feature would falsify the candidate, and what uncertainty would remain if it matched?
```

After checking the image again, replace an uncertain transcription with the corrected reading and retain any unresolved alternatives. Use [add or rewrite](search-patterns.md#add-or-rewrite) when deciding how much previous context to carry forward. If the new search loses its Overview, follow [disappeared after editing](troubleshooting.md#disappeared-after-editing).

## Check the answer

Compare a proposed match with the original challenge evidence. Require agreement on distinctive details such as the junction layout and relative building positions, and identify a feature that would make the candidate impossible. Repeated agreement from similarly worded searches is not independent scene evidence.

Under the strict automatic-Overview rule, a verification search stays in ordinary Google text Search. Opening maps, source pages or image-search tools requires permission in the competition rules; none is a required step in this page. If the permitted information cannot resolve a conflict, record the location as unresolved. An Overview naming a place does not complete that verification.

## Related pages

[Search operators](search-patterns.md#operators) covers targeted wording. [Steganography and decoding chains](stego-misc.md) covers hidden-data questions about image files. [Rules and surfaces](troubleshooting.md#rules-and-surfaces) keeps the search workflow within the permitted interface. Use [missing-Overview recovery](troubleshooting.md#no-overview) when no Overview appears.
