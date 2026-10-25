# Reverse engineering

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Ask about the checker operation or execution behavior you are currently trying to explain. These examples are suggested search wording; Overview appearance is not guaranteed. The toy calculations below were checked offline, which verifies their technical content rather than their triggering behavior. See [sources and evidence](sources.md).

## What to include

Keep the architecture, exact relevant expression, casts, byte widths, signedness, index origin, loop bounds and referenced constants. Include the input routine when input handling matters. For a stateful transformation, preserve the initial state and the update order; a single isolated byte may omit the dependency needed to invert it.

Treat decompiler types as interpretations until the relevant instructions or runtime behavior support them. Separate what you observed from what you suspect. A useful excerpt preserves the operation being questioned without carrying every step of opening and navigating the binary.

## Try this question

For the mechanism:

```text
How can XOR followed by 8-bit addition be inverted, and how can the inverse be checked using the original expression?
```

For a complete small instance:

```text
How do I recover four unsigned input bytes when target[i]=((input[i]^0x5a)+i)&255 for i=0..3 and target=[0,255,1,2] in decimal? Calculate the input bytes in hexadecimal and verify every byte using the original expression.
```

The exact target values make this a calculation rather than an invitation to guess the missing data. If your real array is too large for a readable query, describe its shape and request a method that accepts the full local data. Clearly label any shortened sample as an example; see [large inputs](search-patterns.md#large-inputs).

## If that does not help

If there is [no Overview](troubleshooting.md#no-overview), preserve the decisive expression and ask about one operation or uncertainty. If the query grows after new findings, [add or rewrite](search-patterns.md#add-or-rewrite) according to whether the immediate task has changed.

Once the arithmetic checks but execution fails, move the question to the new observation:

```text
Why does this toy checker reject my input? Its relation is target[i]=((input[i]^0x5a)+i)&255 for i=0..3, with target=[0,255,1,2]. The recovered raw bytes 5a a4 a5 a5 pass the forward calculation. I typed the text 5aa4a5a5, and read(0,buf,4) returned 4. Explain which bytes reached the buffer and what I should inspect next.
```

This update retains the verified result and input boundary. It does not require the previous Search result to supply omitted context. If the answer still overlooks the actual array or input representation, use the [ignored-data guidance](troubleshooting.md#answer-ignores-data).

## Check the answer

For the stated byte relation, undo addition before XOR:

```text
input[i] = ((target[i] - i) & 255) ^ 0x5a
Recovered bytes: 5a a4 a5 a5
Forward result:  00 ff 01 02
```

The mask retains eight bits, giving reduction modulo 256 for this arithmetic. The original toy relation was checked across all 65,536 byte/index combinations over a byte period.

The first four characters of the typed text are bytes `35 61 61 34`; their forward result is `6f 3c 3d 71`. Where debugging is permitted, inspect the actual buffer and input return count. A plausible-looking flag or printable string does not replace a forward check.

## Related pages

Use [Pwn and OS internals](pwn-os.md) for crashes and memory state, [Cryptography](cryptography.md) for mathematical assumptions, or [Steganography and decoding](stego-misc.md) for representation chains. Return to [challenge categories](../README.md#challenge-categories).
