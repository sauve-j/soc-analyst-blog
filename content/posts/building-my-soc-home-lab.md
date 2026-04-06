---
title: "Building a SOC Home Lab from Scratch"
date: 2026-04-06
draft: false
tags: ["lab-setup", "elastic", "siem", "edr", "soc"]
summary: "How I built a full SOC environment with Elastic SIEM, Elastic Defend EDR, Sysmon, Velociraptor, and a Kali attacker machine to simulate real-world investigations."
---

## The Goal

Build a realistic security operations environment where I can simulate attacks, detect them through a SIEM, investigate alerts, and document the full triage process. The same workflow used in production SOCs.

## Architecture

| Machine   | OS           | IP Address | Role                        |
|-----------|--------------|------------|-----------------------------|
| elk-siem  | Ubuntu 22.04 | 10.0.0.10  | Elastic SIEM + Fleet Server |
| win-ep-01 | Windows 10   | 10.0.0.20  | Windows Endpoint            |
| lin-ep-01 | Ubuntu 22.04 | 10.0.0.30  | Linux Endpoint              |
| vr-server | Ubuntu 22.04 | 10.0.0.40  | Velociraptor DFIR Server    |
| kali-atk  | Kali Linux   | 10.0.0.50  | Attacker Machine            |

## Why These Tools

**Elastic Security** as the SIEM because it's widely deployed in enterprise SOCs and the free tier includes detection rules mapped to MITRE ATT&CK out of the box.

**Elastic Defend** for EDR it integrates directly with the SIEM and provides process trees, file events, and network telemetry similar to what you'd see with CrowdStrike or SentinelOne.

**Sysmon** on Windows with the Olaf Hartong modular config for deep process, network, and file visibility that standard Windows logging misses.

**Auditd** on Linux to capture system calls, file access, and command execution, the Linux equivalent of Sysmon.

**Velociraptor** for on-demand forensic collection and threat hunting during investigations.

**Kali Linux** as the attacker machine, running on a separate laptop connected via a dedicated network segment.

## Setup Process

*Detailed setup steps coming in follow-up posts for each component.*

## What's Next

With the environment ready, I'll be running attack simulations using Atomic Red Team and C2 frameworks, then investigating the alerts they generate. Documenting each investigation as a full writeup in my [portfolio](https://github.com/sauve-j/soc-portfolio).