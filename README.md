# UTM-Kali_MSF2_Guide
# UTM Virtual Lab Setup Guide: Kali Linux + Metasploitable 2 (Apple Silicon)

A step-by-step guide to building a cybersecurity practice lab on a Mac with an M-series chip using **UTM**, with **Kali Linux** as the attacker machine and **Metasploitable 2** as an intentionally vulnerable target.

📄 **[Read the guide (PDF)](UTM_Virtual_Lab_Setup_Guideline_Kali_Metasploitable.pdf)**

## Why this guide exists

Most beginner pentesting tutorials assume an Intel PC running VirtualBox. On Apple Silicon (ARM), that doesn't work out of the box: **Metasploitable 2 is x86_64-only and has no official ARM build.**

UTM solves this. It runs ARM guests natively (Kali) and emulates x86_64 for the ones that need it (Metasploitable), so both machines can live in one lab on one laptop.

## What the guide covers

- Installing UTM on macOS
- Deploying **Kali Linux** (ARM64, native virtualization)
- Deploying **Metasploitable 2** (x86_64, emulated), including converting the VMware `.vmdk` disk to `.qcow2` with `qemu-img`
- Lab network configuration and verifying the two VMs can reach each other
- Troubleshooting common UTM issues
- Lab safety, isolation, and cloning (UTM's substitute for snapshots)

## Lab overview

| VM | Role | UTM mode | Suggested resources |
|---|---|---|---|
| Kali Linux | Attacker machine | Virtualize (native ARM64) | 4 GB+ RAM, 2+ cores, 40–60 GB disk |
| Metasploitable 2 | Vulnerable target | Emulate (x86_64) | 512 MB–1 GB RAM, ~10–15 GB disk |

## Requirements

- A Mac with Apple Silicon (M1–M4)
- 8 GB RAM minimum (16 GB recommended)
- ~75 GB free disk space
- A currently supported version of macOS
- [UTM](https://mac.getutm.app/)
- [Homebrew](https://brew.sh/) (for `qemu-img`)
  

## Where to get the images

| VM | Official source |
|---|---|
| Kali Linux | https://www.kali.org/get-kali/#kali-installer-images (choose Apple Silicon / ARM64) |
| Metasploitable 2 | https://sourceforge.net/projects/metasploitable/ |

## Notes

- Metasploitable runs through software emulation, so expect it to be slower than the native Kali VM.
- UTM has no built-in snapshots. Use **Clone** to save a clean baseline of each VM.

## ⚠️ Safety and responsible use

Metasploitable 2 is **intentionally vulnerable**. Keep it on an isolated network and never expose it to the internet, or to a home, campus, or production network. Never enter real credentials or personal data into any lab VM.

Everything in this guide is for **authorized, educational, and defensive purposes only**, against machines you own or have explicit permission to test.

## Author

**Dan Gabriel B. Romulo**, CYLSEC

Feedback and suggestions are welcome. Feel free to open an issue if something doesn't work on your setup (please include your Mac chip and macOS version).
