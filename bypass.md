# Rootkit Bypass Technique (LD_PRELOAD)

## Objective
Bypass a userland rootkit that intercepts libc functions using `LD_PRELOAD`,
allowing accurate filesystem inspection and artifact recovery.

## Technique Overview
The rootkit injects a malicious shared object into every dynamically linked
process by abusing `/etc/ld.so.preload`. This enables function hooking
(e.g. `readdir`, `readdir64`, `fopen`) to hide files and directories.

To bypass this behavior, commands were executed with a clean environment,
preventing the dynamic loader from applying the malicious preload.

## Bypass Method

Execute binaries without inherited environment variables:

```bash
env -i ls -la /
```
<img width="890" height="456" alt="image" src="https://github.com/user-attachments/assets/73d6e781-66dc-4aeb-b7e7-117ea4444813" />

<img width="1081" height="553" alt="image" src="https://github.com/user-attachments/assets/66f363a6-6223-42f5-8c0f-145352813a30" />

## Validation
The bypass was validated by comparing command output:

- Standard execution (`ls -la /`) showed filtered results
- Clean execution revealed hidden artifacts

The discrepancy confirms active userland manipulation.

## Why This Works
`LD_PRELOAD` is controlled through environment variables and loader
configuration. Clearing the environment prevents the malicious shared object
from being loaded, restoring original libc behavior.

## Defensive Insight
This technique is effective during incident response to:
- Detect userland rootkits
- Bypass basic evasion mechanisms
- Perform filesystem validation without specialized forensic tooling
