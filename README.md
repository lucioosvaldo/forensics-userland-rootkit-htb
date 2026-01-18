# Userland Rootkit Detection & Analysis (LD_PRELOAD Abuse)

## Overview
This project documents the forensic analysis of a Linux userland rootkit abusing `LD_PRELOAD`
to hide files and manipulate libc functions such as `readdir` and `fopen`.

The objective was to detect the persistence mechanism, bypass userland hooks,
and recover hidden artifacts without relying on full forensic toolsets.

## Threat Summary
- Persistence via `/etc/ld.so.preload`
- Malicious shared object injected into all processes
- Hooked functions:
  - `readdir`
  - `readdir64`
  - `fopen`
- Selective hiding of directories and files based on string matching

## Detection Techniques
- Behavioral anomalies in `ls` vs `ls -la`
- Inspection of `/etc/ld.so.preload`
- Dynamic loader abuse identification
- Comparison of execution with and without environment variables

## Rootkit Bypass Strategy
- Execution of binaries using `env -i`
- Direct filesystem enumeration bypassing libc hooks
- Controlled removal of preload configuration for validation

## Findings
- Hidden directory: `/var/pr3l04d_/`
- Flag stored in a filtered file
- Rootkit logic confirmed via binary string analysis

## Skills Demonstrated
- Linux Forensics
- Userland Rootkit Detection
- LD_PRELOAD Abuse Analysis
- Blue Team / DFIR Methodology
- Adversary Evasion Techniques

## Disclaimer
This project is based on a controlled lab environment for educational purposes.
No production systems were harmed.
