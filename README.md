# AWS Honeypot Investigation — Cowrie, Dionaea & Wazuh

A hands-on security monitoring and threat investigation project built on AWS EC2. The environment used **Cowrie** to capture SSH interactions, **Dionaea** to collect activity against emulated services, and **Wazuh** to support log searching and analysis.


## Project overview

- **Infrastructure:** Separate AWS EC2 systems for the Cowrie and Dionaea sensors and the Wazuh analysis server.
- **Collection:** SSH events and session artifacts from Cowrie; connections and captured files from Dionaea.
- **Evidence handling:** Sensor archives exported to a local Linux environment and checked using SHA-256.
- **Investigation:** Prioritization of noisy sources, examination of Cowrie event records, threat-intelligence correlation, and preliminary triage of captured file hashes.

## Main findings

### Automated SSH activity

An investigation of repeated activity from `183.23.147.89` identified:

- SSH client banner: `SSH-2.0-Go`
- HASSH client fingerprint: `01ca35584ad5a1b66cf6a9846b5b2821`
- Repeated shell probe: `echo -e "\x6F\x6B"`

The combination matched indicators described in published **IntrusionLabs research** on a Go-based SSH credential-testing tool. This supports a tooling/behavior similarity assessment; it **does not** prove the same operator, binary, or campaign.

### Captured-file triage

Seven distinct SHA-256 values were documented from selected captured files: **two from Dionaea** and **five from Cowrie**. VirusTotal findings were used for preliminary classification and to identify questions for further investigation. Detection labels and automated summaries are **not** treated as proof that the reported capabilities executed on the honeypot hosts.

## Investigation status and limitations

- Cowrie SSH investigation documented; Dionaea log analysis remains incomplete.
- Captured files have not yet been correlated to their individual source connections or transfer sessions.
- No host compromise, successful exploitation, or independent malware reverse engineering is claimed.
- A session-level correlation/detection approach is proposed but not yet deployed or validated.

## Future work

1. Complete Dionaea connection and delivery-path analysis.
2. Correlate file hashes with original timestamps and connection/session identifiers.
3. Develop and evaluate detection logic for the observed SSH behavior.

## Report

The PDF contains architecture and collection details, Wazuh evidence, the IntrusionLabs comparison, and seven captured-file assessments, along with sources and important limitations.

> This repository contains research documentation only. It does not distribute captured malware samples, secrets, or raw unfiltered sensor logs.
