# network-to-forensics

A hands-on progression from networking fundamentals to digital forensics,
built as one connected case. Every artifact here is something I ran on my
own hardware, with machine-generated evidence attached.

## Scope

All targets in this repository are hardware I own, isolated on an internal
lab VLAN. No third-party systems are involved at any point.

## Structure

The repo climbs four rungs, in order, and the rungs link into a single case:

- **00-lab/** — lab build, topology, VLAN segmentation, isolation proof
- **01-foundation/** — networking and systems fundamentals, each with a
  recorded baseline of what normal looks like
- **02-offense/** — attacker actions against owned lab targets, timestamped
  as ground truth
- **03-defense/** — detection of those exact actions against the recorded
  baselines, then hardening, then re-testing
- **04-forensics/** — imaging and timeline reconstruction from evidence
  alone, scored against the offense record

Each artifact is a folder with a README and an `evidence/` directory.
The format is defined in `_template/artifact-template.md`.