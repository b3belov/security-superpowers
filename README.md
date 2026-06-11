# Security Superpowers

Security Superpowers is a Codex plugin that packages a large collection of cybersecurity skills for analysis, investigation, detection, response, and testing workflows.

The plugin is intended for security teams, incident responders, detection engineers, threat hunters, cloud security engineers, DFIR practitioners, red teamers, purple teamers, and application security teams who want repeatable Codex workflows for common security tasks.

## What Is Included

- 754 primary Codex skills
- 760 `SKILL*.md` files, including localized variants
- 754 bundled `references/` directories
- 754 bundled `scripts/` directories
- 280 bundled `assets/` directories
- A Codex plugin manifest at `.codex-plugin/plugin.json`

The collection covers defensive operations, security engineering, and authorized assessment workflows across cloud, identity, endpoint, network, application, mobile, OT/ICS, malware, forensics, and governance domains.

## Repository Layout

```text
security-superpowers/
├── .codex-plugin/
│   └── plugin.json
├── skills/
│   └── <skill-name>/
│       ├── SKILL.md
│       ├── LICENSE
│       ├── references/
│       ├── scripts/
│       └── assets/
└── README.md
```

Each skill folder is self-contained. The `SKILL.md` file contains the trigger metadata and workflow instructions; `references/` holds supporting material that Codex can load when needed; `scripts/` holds reusable helper code; `assets/` holds templates or other bundled files for applicable workflows.

## Plugin Metadata

The plugin manifest declares:

- Plugin name: `security-superpowers`
- Display name: `Security Superpowers`
- Category: `Security`
- License: `Apache-2.0`
- Skills path: `./skills/`

The plugin metadata includes discovery keywords for:

- incident response
- threat intelligence
- forensics and DFIR
- detection engineering
- threat hunting
- malware analysis and reverse engineering
- cloud security
- identity security and Active Directory
- Kubernetes and container security
- vulnerability management
- penetration testing
- red team and purple team workflows
- OT/ICS security
- mobile, API, and application security
- supply chain security
- ransomware analysis and response
- OSINT and IOC enrichment

## Skill Coverage

The current collection spans these major subdomains:

| Subdomain | Skill Count |
| --- | ---: |
| cloud-security | 63 |
| threat-hunting | 56 |
| threat-intelligence | 50 |
| network-security | 43 |
| web-application-security | 42 |
| malware-analysis | 39 |
| digital-forensics | 37 |
| soc-operations | 33 |
| identity-access-management | 33 |
| container-security | 29 |
| security-operations | 28 |
| ot-ics-security | 28 |
| api-security | 28 |
| incident-response | 26 |
| vulnerability-management | 25 |
| red-teaming | 24 |
| penetration-testing | 20 |
| devsecops | 17 |
| zero-trust-architecture | 17 |
| endpoint-security | 17 |
| phishing-defense | 15 |
| cryptography | 15 |
| mobile-security | 13 |
| ransomware-defense | 13 |
| threat-detection | 7 |
| application-security | 4 |
| compliance-governance | 4 |
| supply-chain-security | 3 |
| deception-technology | 3 |
| ai-security | 2 |

Common tags include `threat-hunting`, `mitre-attack`, `threat-intelligence`, `cloud-security`, `penetration-testing`, `network-security`, `incident-response`, `owasp`, `forensics`, `soc`, `api-security`, `zero-trust`, `web-security`, `ot-security`, `active-directory`, `red-team`, `siem`, `compliance`, `phishing`, `malware-analysis`, `aws`, `scada`, `ransomware`, and `kubernetes`.

## Example Workflows

Security Superpowers can help Codex with tasks such as:

- triaging suspicious alerts and mapping evidence to MITRE ATT&CK
- building SIEM queries and detection rules
- enriching indicators of compromise
- reconstructing incident timelines
- analyzing Windows, Linux, browser, memory, email, and cloud artifacts
- reviewing Kubernetes, container, and cloud security configurations
- planning vulnerability management and remediation workflows
- analyzing malware behavior, persistence, C2, and sandbox output
- creating ransomware response playbooks
- supporting authorized red team or purple team exercises
- auditing identity, access, and zero trust controls
- documenting post-incident lessons learned

The plugin starter prompts are:

```text
Triage a security alert, map ATT&CK techniques, and draft response steps.
Hunt across cloud, identity, endpoint, and network logs for compromise.
Analyze malware or forensic artifacts and extract actionable indicators.
```

## Installation

This repository is already structured as a Codex plugin root. The plugin manifest is:

```text
.codex-plugin/plugin.json
```

For a local Codex marketplace workflow, clone the repository into the marketplace plugin directory:

```bash
git clone https://github.com/b3belov/security-superpowers.git ~/plugins/security-superpowers
```

Then make sure your personal marketplace file includes an entry for the plugin:

```json
{
  "name": "security-superpowers",
  "source": {
    "source": "local",
    "path": "./plugins/security-superpowers"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Security"
}
```

For the default personal marketplace path, that marketplace file is usually:

```text
~/.agents/plugins/marketplace.json
```

After the marketplace entry exists, install or refresh the plugin in Codex with the marketplace name configured in that file, for example:

```bash
codex plugin add security-superpowers@personal
```

Start a new Codex thread after installing or refreshing the plugin so Codex reloads plugin metadata and skill entries.

## Skill Format

Every primary skill uses Codex skill frontmatter with the fields accepted by the skill validator:

```yaml
---
name: example-skill-name
description: Short trigger-oriented description
license: Apache-2.0
metadata:
  domain: cybersecurity
  subdomain: threat-hunting
  tags:
    - threat-hunting
    - mitre-attack
---
```

Cybersecurity taxonomy fields such as `domain`, `subdomain`, `tags`, `mitre_attack`, `nist_csf`, `d3fend_techniques`, `atlas_techniques`, and `nist_ai_rmf` are stored under `metadata` so the skills remain compatible with Codex skill validation.

## Validation

The current repository has been validated with the Codex plugin and skill validators:

```text
Plugin validation: passed
Skill validation: 754 passed, 0 failed
```

During development, validate the plugin root with the plugin creator validator from your Codex skill installation:

```bash
python3 /path/to/plugin-creator/scripts/validate_plugin.py /path/to/security-superpowers
```

To validate an individual skill:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py /path/to/security-superpowers/skills/<skill-name>
```

If your local Python environment does not include YAML support, install or provide `PyYAML` for the validation run.

## Adding Or Updating Skills

When adding a new skill:

1. Create a folder under `skills/` using lowercase hyphen-case.
2. Add a required `SKILL.md`.
3. Keep top-level frontmatter limited to validator-supported fields.
4. Store cybersecurity taxonomy under `metadata`.
5. Add only resources that directly support the skill, such as `references/`, `scripts/`, or `assets/`.
6. Validate the skill before committing.
7. Validate the whole plugin before publishing changes.

Keep skill descriptions trigger-oriented. Codex sees `name` and `description` before it decides whether to load a skill, so descriptions should clearly state what the skill does and when to use it.

## Safety And Authorized Use

This repository includes skills for both defensive security work and authorized assessment workflows. Some skills discuss exploitation, red team tooling, malware analysis, credential exposure, and attack simulation.

Use these workflows only on systems, accounts, networks, applications, and data where you have explicit permission. Do not use the offensive or simulation material for unauthorized access, persistence, evasion, credential theft, data exfiltration, or disruption.

For public sharing, examples in this repository are intended to be placeholders or training artifacts. Review any local modifications before publishing or importing into a production environment.

## License

The plugin manifest declares `Apache-2.0`. Each skill folder also includes a `LICENSE` file.

## Repository

GitHub: https://github.com/b3belov/security-superpowers
