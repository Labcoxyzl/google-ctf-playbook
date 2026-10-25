# Network forensics

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Ask about the layer that currently fails. A useful search identifies what was captured, how it was exported and which transformations have already succeeded. Keep those facts when you revise the question.

## What to include

| Detail | Why it matters |
| --- | --- |
| Protocol and version | HTTP/1.1 chunk framing does not describe every HTTP version or protocol. |
| Stream direction | Record server-to-client, client-to-server or both; a mixed conversation needs message boundaries. |
| Export representation | Raw bytes, displayed text, hexadecimal text and an exported object can represent different processing stages. |
| Headers and framing | Preserve the exact transfer and content encodings and whether headers remain in the file. |
| Boundary lengths and errors | Record byte counts after each transformation, the decoder and its exact error. |
| Capture completeness | Keep relevant TCP reassembly or missing-data observations separate from assumptions about the export. |

For a raw HTTP/1.1 response containing headers, `Transfer-Encoding: chunked` and `Content-Encoding: gzip`, identify the response boundary, separate headers from the body, remove chunk framing, then decompress the resulting gzip bytes. An export that already removed framing needs a different starting point. The [source notes](sources.md) distinguish the locally checked framing example from an operational HTTP parser.

## Try this question

The examples are suggested wording. These exact searches have not been tested live and do not guarantee an Overview.

A general mechanism question:

```text
What is the decoding order for an HTTP/1.1 response with chunked transfer framing and gzip content encoding?
```

A question with the relevant export conditions:

```text
How should I decode an HTTP/1.1 response exported from Wireshark as raw server-to-client bytes? The file contains response headers followed by the body. The headers include Transfer-Encoding: chunked and Content-Encoding: gzip. Explain message boundaries, decoding order and checks that distinguish a complete response from an incomplete export.
```

## If that does not help

Once dechunking succeeds, rewrite around the decompression failure. Preserve the completed work and the remaining uncertainty:

```text
How should I diagnose an incomplete gzip member from an HTTP/1.1 CTF capture? I exported raw server-to-client bytes, separated the response headers and decoded chunked framing. The resulting bytes start 1f8b08, but Python gzip.decompress raises EOFError. Which observations distinguish an incomplete export, missing captured TCP data and incorrect message boundaries? Give a check and expected result for each case.
```

Add your measured lengths and full error text when available. If the Overview vanishes after this update, use [disappeared after editing](troubleshooting.md#disappeared-after-editing). If it repeats the initial procedure, use [answer ignores data](troubleshooting.md#answer-ignores-data) and ask it to account for the completed dechunking step.

## Check the answer

A gzip header identifies a possible format; it does not establish that the member is complete. The primary handoff's truncated local fixture retained `1f8b08` while raising `EOFError`.

Check chunk sizes against the actual byte spans and account for the terminating chunk and trailer boundary. Compare the exported response with available stream-reassembly evidence before blaming compression. Validate successful decompression using the decoder's integrity checks and the expected output structure. A readable prefix alone does not verify the whole object.

## Related pages

[Disk and memory forensics](disk-memory-forensics.md) covers artifact correlation. [Steganography and decoding chains](stego-misc.md) covers representation changes. [Current-question wording](search-patterns.md#current-question) helps carry a verified layer into the next search. Return to [missing-Overview recovery](troubleshooting.md#no-overview) when ordinary results contain no Overview.
