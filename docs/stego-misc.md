# Steganography and decoding chains

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Describe an extraction so another person could reproduce the same bytes. Then ask about the first unexplained boundary in the decoding chain. A recognizable prefix or a detector's guess helps choose a check; it does not establish that the extraction is correct.

## What to include

| Stage | Facts to preserve |
| --- | --- |
| Original artifact | Actual format, dimensions, color type and available channels. |
| Bit selection | Channel or channel sequence, bit plane and any inversion. |
| Traversal | Pixel order, starting offset and whether rows or columns come first. |
| Packing | Bits per output byte and whether the first extracted bit becomes the most or least significant bit. |
| Transformations | Exact decoding order, including text-to-byte conversions, decompression or decryption already attempted. |
| Each boundary | Output byte count, a short hexadecimal prefix and structural checks. |
| Current failure | Decoder name, relevant options and exact exception or error text. |

Keep encoded text and decoded bytes distinct. A printed hexadecimal representation is text until it is converted back to bytes. If your chain is Base64 text, decoded bytes and then decompression, record the input and output length at each step. Avoid silently decoding a layer twice.

## Try this question

The examples are suggested wording. These exact searches have not been tested live and do not guarantee an Overview. The primary handoff contains no completed steganography Overview trial; see the [source notes](sources.md).

A general question:

```text
How can I distinguish meaningful PNG bit-plane extraction from accidental file-signature matches?
```

A concrete hypothetical extraction, whose values should be replaced with your measurements:

```text
How can I evaluate this PNG CTF extraction? The image is 128 by 128 pixels with RGB channels. I took bit 0 of the red channel, moving left to right across each row and top to bottom. I packed the first extracted bit as the most significant bit of each output byte. The result is 2048 bytes beginning 1f8b08. Which format checks test this result, and which extraction assumptions remain unverified?
```

The stated dimensions and one-bit-per-pixel extraction account for the 2048-byte output. That length agreement checks the extraction description; it does not validate the hidden message.

## If that does not help

Carry a failed decoder forward as an observation:

```text
Why does Python gzip.decompress raise EOFError on this hypothetical CTF extraction? A 128 by 128 RGB PNG yields 2048 raw bytes using red-channel bit 0, row order left to right and top to bottom, first bit packed as the most significant bit. The bytes begin 1f8b08 and repeat identically on extraction. No text decoding was applied. Which checks distinguish an incomplete compressed member from incorrect extraction parameters or message boundaries?
```

Use your actual full error text. If earlier steps involved Base64 or another transformation, include those verified boundaries too. When the answer ignores a completed step, use [answer ignores data](troubleshooting.md#answer-ignores-data). When adding the error removes the Overview, use [disappeared after editing](troubleshooting.md#disappeared-after-editing).

## Check the answer

Reproduce the output with the recorded parameters. Inspect format structure beyond the initial signature, including declared lengths, terminators and integrity fields where the format provides them. Check that successful decoding consumes the intended message and yields a structurally plausible result. Readable fragments alone are weak evidence.

Change one uncertain extraction choice at a time and record what differs. If several choices remain plausible, ask for a distinguishing observation rather than selecting the output that merely resembles an expected flag.

## Related pages

[Network forensics](network-forensics.md) covers framing and gzip completeness. [Cryptography](cryptography.md) covers construction and sample relationships. [Large inputs](search-patterns.md#large-inputs) explains how to describe data without pretending a prefix is the complete artifact. Return to [missing-Overview recovery](troubleshooting.md#no-overview) when no Overview appears.
