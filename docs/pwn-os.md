# Pwn and OS internals

[Home](../README.md) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Describe the observed crash or operating-system behavior precisely, then ask which observation would distinguish the remaining explanations. These queries are suggested wording, with no guaranteed Overview appearance. The handoff contains exploratory crash-related searches, not a validated exploit chain; see [sources and evidence](sources.md).

## What to include

Carry the architecture and ABI, relevant input routine, buffer size or known offsets, return value and exact crash instruction. State which mitigations were inspected and which memory or register values were actually observed. A debugger's current instruction pointer, a saved return-address slot and bytes inside an input buffer are different evidence.

For an operating-system question, include the system-call arguments, return value, error code, relevant permissions and execution context. Preserve uncertainty about state that you have not inspected. Names such as “stack overflow” or “canary bypass” should describe what the evidence supports.

## Try this question

For the general mechanism:

```text
What does reaching __stack_chk_fail in a Linux ELF program establish, and what additional observations are needed to determine whether a saved return address changed?
```

For a more specific diagnostic question:

```text
How should I investigate guard corruption in a local x86-64 Linux CTF binary using the System V ABI? After an oversized input, the saved stack canary differs from its value at function entry and the compiler's guard check reaches __stack_chk_fail. NX is enabled. I have not inspected the saved return-address slot. Explain useful GDB observation points around the input operation and guard check, and what each observation would establish.
```

In your own query, add the actual input call, buffer location and relevant instruction slice when known. Do not invent offsets to make the question look complete. Ask for the observations needed to determine them.

## If that does not help

If there is [no Overview](troubleshooting.md#no-overview), isolate the immediate mechanism: guard checking, input length, a permission failure or an address calculation. Retain the accurate security terminology; [clearer wording](search-patterns.md#terminology) is not a keyword-evasion technique.

When a new memory observation arrives, [update the current question](search-patterns.md#add-or-rewrite). For example:

```text
What does this updated crash evidence establish in a local x86-64 Linux CTF binary? After the input operation, the saved canary changed, while the saved return-address slot still equals its value at function entry. Execution aborts at the guard check before the function returns. Explain what this run shows about corruption and return-address control, and which memory boundaries I should inspect next.
```

This remains a self-contained normal search. It replaces the unknown slot state with an observation without assuming that other inputs would behave identically. If the response claims control that these facts do not establish, use the [ignored-data guidance](troubleshooting.md#answer-ignores-data).

## Check the answer

A mismatching saved guard on the compiler's guard-check path establishes detected guard corruption. It does not identify the corrupting write, prove a particular overflow layout, or demonstrate control of the saved return address. Seeing the `__stack_chk_fail` symbol alone is weaker; inspect its caller and the actual check where the competition permits debugging.

Compare relevant memory before and after the suspected operation, including the input return count and first known changed location. A watchpoint or breakpoint plan should explain what its observation proves. Do not accept “the crash instruction pointer contains my input” unless the register evidence actually shows that.

NX concerns executable memory permissions; it does not prevent writes beyond a buffer. PIE and ASLR concern aspects of address layout. Ask which mitigation matters to the current observation instead of treating their names as a complete exploitability assessment.

## Related pages

Use [Reverse engineering](reverse-engineering.md) to resolve instruction or type semantics, [Web](web.md) for application authorization, or [Disk and memory forensics](disk-memory-forensics.md) for evidence in captured artifacts. Return to [challenge categories](../README.md#challenge-categories).
