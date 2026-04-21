---
title: "Adding the Endpoints"
date: 2026-04-11
draft: false
tags: ["lab-setup", "elastic", "sysmon", "auditd", "windows", "linux"]
summary: "Two new VMs and both shipping logs into the SIEM."
---

The SIEM was up but it had nothing to look at. I added two endpoints so it actually has something to ingest: a Windows 11 VM and an Ubuntu Server VM, both running in VirtualBox on bridged networking.

The Windows side got Sysmon with Olaf Hartong's modular config, PowerShell Script Block Logging turned on, and the Elastic Agent enrolled into Fleet. I also disabled Windows Defender on this VM so   it doesn't block attack simulations I'll do later from my kali linux laptop.

The Linux side got Auditd with Florian Roth's ruleset, which gives a solid baseline of execve, file watch, and network rules out of the box. Then the Elastic Agent on top of that.

I also set up DHCP reservations on my router for all three VMs so the IPs stop changing on me, I forgot the first time so I had to change the ip everywhere (oups).

![Endpoints Healthy](FleetHealthy2.png)

Three machines reporting in now: the ELK server, the Windows endpoint, and the Linux endpoint. The next step is building a triage dashboard in Kibana and enabling some detection rules so I can finally start receiving alerts.
