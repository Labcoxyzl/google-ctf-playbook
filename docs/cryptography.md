# Cryptography

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Give the construction and its assumptions before asking which recovery method applies. These examples are suggested wording with no guaranteed Overview appearance. The bounded RSA example was checked offline; that validates the mathematics, not a search trigger. See [sources and evidence](sources.md).

## What to include

State the scheme or exact relation, encoding and padding, sample count, known values, unknown values and any justified message bound. For multiple samples, identify shared or different keys, nonces, moduli and messages. An oracle is available only if you can actually make the relevant observation.

Keep numeric bases and byte order explicit. A truncated integer cannot support an exact numerical recovery. Use a complete toy example for a method question, or request a solver that accepts the full local values; see [large inputs](search-patterns.md#large-inputs).

## Try this question

For a broad diagnostic question:

```text
Why can a direct integer cube root fail for unpadded RSA with e=3, and what assumptions distinguish direct recovery from modular reduction?
```

For a complete instance with a useful bound:

```text
How can I recover m in this toy unpadded RSA instance: e=3, n=11413, c=5610, c=m^3 mod n, and 0<=m<64? The integer cube root of c is not exact. Derive a finite range for k in m^3=c+k*n, find valid m, and verify by modular exponentiation.
```

The bound supplies information that the general question lacks. For other constructions, provide the corresponding relationships: nonce reuse needs the key and mode conditions; related-message reasoning needs the actual relationship. Keep encryption, hashing, encoding and compression distinct.

## If that does not help

If there is [no Overview](troubleshooting.md#no-overview), ask one question about the method's preconditions while preserving the facts that determine them. If adding samples changes the applicable method, [rewrite the current question](search-patterns.md#add-or-rewrite) with the complete sample relationships.

After arithmetic succeeds, an output-format problem deserves its own query:

```text
In a toy unpadded RSA problem, m=42 verifies 42^3 mod 11413=5610. The minimal unsigned big-endian representation is the single byte 2a, but the original message encoding and required byte length are unspecified. What can I infer about the plaintext representation, and which missing format facts would distinguish the possibilities?
```

This asks for the remaining uncertainty instead of assuming that the recovered integer must already be a readable flag. If the answer overlooks a supplied bound or sample relationship, request a calculation dependent on that fact; see [ignored data](troubleshooting.md#answer-ignores-data).

## Check the answer

For the stated toy problem, `0 <= m <= 63` implies `m^3 <= 63^3`. Since `m^3 = 5610 + k*11413`, candidates need only cover:

```text
0 <= k <= floor((63^3 - 5610) / 11413) = 21
k = 6 gives 5610 + 6*11413 = 74088 = 42^3
42^3 mod 11413 = 5610
```

The unique candidate within the stated message bound is `m=42`. An exact integer-root check and the original modular relation validate the result where local calculation is permitted. This finite search depends on the small bound; it is not a general RSA recovery method.

A failed direct root alone does not establish padding, a particular attack or an implementation bug. Check the supplied assumptions before accepting the explanation. For this direct recovery method, an unpadded representative satisfying `m^3<n` avoids modular reduction.

## Related pages

Use [Reverse engineering](reverse-engineering.md) when recovering the actual construction from code, or [Steganography and decoding](stego-misc.md) when the remaining problem concerns byte representation. Return to [challenge categories](../README.md#challenge-categories).
