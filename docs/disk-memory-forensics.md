# Disk and memory forensics

[Home](../README.md#challenge-categories) · [Troubleshooting](troubleshooting.md) · [Search patterns](search-patterns.md)

Ask which explanations fit the records and which additional artifact would distinguish them. A mismatch between timestamps or process views is a starting point for investigation, not proof of tampering.

The questions below are suggested wording with no guaranteed Overview appearance. The concrete records are fictional teaching examples, not findings from an examined image. Replace them with the relevant rows from your challenge.

## What to include

| Keep | Why it matters |
| --- | --- |
| Artifact type and acquisition context | A disk image, memory image and exported report contain different evidence. |
| OS/build, filesystem and tool/plugin version | Interpretation depends on the structures and parser used. |
| Object identifiers and addresses | Names alone do not establish that two rows describe the same object. |
| Timestamp field names and time basis | Creation, modification, execution and observation times are different facts. |
| Minimal correlated rows and exact errors | These let the answer address the discrepancy you actually observed. |

Preserve the original timestamp value alongside any conversion. State whether a time zone is known, inferred or unknown. Explain why records were joined; matching filenames or process names alone is insufficient.

## Try this question

### Disk timelines

Start with the relationship between artifacts:

```text
How do NTFS MFT timestamps and USN journal records differ in forensic timelines?
```

Then provide a bounded comparison. This example supplies normalized times and a common file reference, while leaving the cause open:

```text
How should I interpret this fictional NTFS timeline? All times are UTC on 2026-01-01. Records resolve to file reference 42:3. The MFT Standard Information modification time is 10:00:00; the File Name modification time is 09:00:00. USN records show RENAME_OLD_NAME for draft.txt and RENAME_NEW_NAME for final.txt at 10:05:00. Which explanations fit these facts, what do they not prove, and which additional artifact would distinguish them?
```

For a real search, add the parser/version and any acquisition or clock uncertainty that changes the interpretation. A rename record should not silently become an explanation for every timestamp difference.

### Memory views

Begin with the distinction between enumeration methods:

```text
Why can process-list and memory-scan results differ in a Windows memory image?
```

Then identify the object and the missing correlation:

```text
How should I interpret a process-view discrepancy in a CTF memory image? In the same image, a memory scan reports PID 4120 at object address 0xffff800000001000 with name worker.exe. Linked-list enumeration has no row at that address. Another listed process has the same name but PID 5280. OS/build, plugin compatibility and exit state are not yet confirmed. What explanations remain, and which next artifact or compatibility check would distinguish them?
```

Do not conceal missing build or plugin information. Once known, include it in the next search. A shared name does not merge the two objects into one process.

## If that does not help

If the [Overview disappears after adding context](troubleshooting.md#disappeared-after-editing), keep one discrepancy, the identifiers needed to correlate it, and the latest relevant observation. Move the full timeline or plugin output into your local notes.

When a new artifact resolves an uncertainty, [rewrite the current question](search-patterns.md#add-or-rewrite). For example, if an exit-time field is now available, ask how it changes the competing explanations instead of continuing to call the object hidden.

## Check the answer

Verify that compared rows refer to the same object and compatible time basis. Check parser support and retain uncertainty about acquisition, incomplete records and clock conversion. Prefer an explanation that predicts a distinguishing observation over one that merely labels a discrepancy suspicious.

The [source notes](sources.md) explain the research evidence and its limits. No real disk or memory image was examined for this page.

## Related pages

Use [network forensics](network-forensics.md) to correlate captured traffic, [pwn and OS internals](pwn-os.md) for memory structures, and [OSINT](osint.md) when attribution requires independent public evidence.
