---
id: 01-foundation/hardware-teardown-component-id
rung: 1
date: 2026-08-31
case: CASE-001
detects:
baseline-for:
reconstructs:
gaps: []
---

# Target machine survey — pre-acquisition recon and live-OS baseline

## Claim

I can survey a target machine's disk, encryption state, and live-OS baseline
before physical acquisition, and identify the acquisition hazards — RST-paired
storage and BitLocker — that would brick a naive image.

## Setup

- Target: HP ENVY x360 Convertible 15m-dr1xxx, broken screen, external HDMI
  display. Windows 11 Home, build 26200. Designated lab evidence target.
- Storage: Intel Optane + 238GB NAND presented as a single 256GB RST volume
  (BusType: RAID).
- Capture: PowerShell 5.1 transcripts run locally on the target, copied off,
  redacted per repo OPSEC checklist, then committed.

## What I did

1. Pulled disk identity: `Get-Disk`, `Get-PhysicalDisk` — recorded volume
   layout, size, partition style, bus type.
2. Checked encryption state: `manage-bde -status` — BitLocker ON, XTS-AES 128,
   used-space-only, TPM + numerical password protectors.
3. Exported the BitLocker recovery key (`manage-bde -protectors -get C:`) and
   stored it in the password vault. The key does not appear in this repo.
4. Captured a live-OS baseline in one transcript: system identity, local
   accounts, installed software, running processes and services, partition and
   volume layout, network adapters and IPv4 addresses.
5. Redacted both transcripts (hostname, username, BIOS serial, MAC addresses,
   home-LAN address) and verified zero hits by search before commit.

## Evidence

- `evidence/junk-laptop-recon.txt` — disk identity and BitLocker status
- `evidence/junk-laptop-baseline.txt` — full live-OS baseline

## What I saw and why

*Pending — four-pass writeup after teardown (2026-09-01).*

## Where it broke

*Pending — teardown (2026-09-01).*

## What normal looks like

*Pending — completed with teardown. Baseline transcript captured; narrative
block to follow.*

## Why it matters for forensics

This machine becomes a rung-4 imaging target. The survey found two hazards
before they could cost the case: the RST pairing means a cold drive pull may
not read as a normal disk, and BitLocker means an image without the recovery
key is ciphertext. Both were found while the machine still boots — which is
the only time they're cheap to solve.

---
Rung: 1 · Date: 2026-08-31 · Status: THIN — blocks 6–8 pending teardown