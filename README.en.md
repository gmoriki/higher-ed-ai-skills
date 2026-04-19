# higher-ed-ai-skills

Open-source AI skills for higher education administration, structured as skill.md files.

*Japanese version / 日本語版: [README.md](README.md)*

---

## What is this?

Between Japanese university operations and generative AI, translation is required. The tacit knowledge of universities — how proposals move through committees, how exceptions in the academic calendar are handled, how authority is split between faculty and staff — is rarely documented, so it does not transfer naturally to AI prompts. This repository publishes the decision frameworks that Ginga Moriki has developed in higher ed × AI work in Japan, packaged as `skill.md` files that anyone can reuse.

**About the author:** Ginga Moriki works at the intersection of higher education administration and AI adoption in Japan. He translates between the operational realities of university staff and the capabilities of modern AI systems — designing practical frameworks, delivering training programs, and publishing tools that help institutions move from policy to practice. See [gmoriki.com](https://gmoriki.com) for details.

**About the open edition:** All content in this repository is **freely usable under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)**. The principles, decision frameworks, and design philosophy are written to be applicable as-is in real university workflows. Paid consulting and advisory services — adapting these frameworks to specific governance structures, drafting internal proposals, running staff training — are offered separately at [gmoriki.com](https://gmoriki.com).

### Where to start

| Reader | Start here |
|---|---|
| University staff (practical use) | → [Available skills](#available-skills) — start with `confidential-info-guidelines` |
| Consultants & researchers | → [DESIGN.md](DESIGN.md) (design philosophy and five principles) |
| Japanese speakers | → [README.md](README.md) |
| Without a GitHub account | → Top of [docs/how-to-use.md](docs/how-to-use.md) |

---

## Available Skills

### Ready to use

| Skill | One-line description | Audience | Version | Links |
|---|---|---|---|---|
| **confidential-info-guidelines** | Decision framework for whether confidential information can be fed to generative AI services (3-level classification) | University staff | v1.1.0 | [SKILL.md](skills/confidential-info-guidelines/SKILL.md) / [examples/](skills/confidential-info-guidelines/examples/) |

### Coming soon

| Skill | One-line description | Target version |
|---|---|---|
| ai-report-evaluation | Evaluation criteria and verification procedures for AI-generated reports | v0.3 |
| tool-selection-guide | AI tool selection checklist tailored to university operations | v0.3 |
| advanced-prompting-for-admin | Applied prompt library for administrative work | v0.4 |
| ai-news-curation | Curation methods for the higher ed × AI information landscape | v0.4 |
| case-library-ai-usage | Library of AI adoption cases from other universities | v0.5 |

### Domain skills (in preparation)

Directories are reserved under [`domain-skills/`](domain-skills/) for department-specific skills (v0.3 and later):
[academic-affairs](domain-skills/academic-affairs/) / [international-office](domain-skills/international-office/) / [ir-analysis](domain-skills/ir-analysis/) / [public-relations](domain-skills/public-relations/) / [research-support](domain-skills/research-support/) / [student-support](domain-skills/student-support/)

---

## How to use

1. **Read directly** — open [SKILL.md](skills/confidential-info-guidelines/SKILL.md) and follow the decision flow for real-world judgment calls
2. **Feed into an AI assistant** — paste as a system prompt or knowledge file in Claude / ChatGPT / Microsoft Copilot
3. **Use in training materials** — freely remix under CC BY-SA 4.0 (share derivatives under the same license)

See **[docs/how-to-use.md](docs/how-to-use.md)** (GitHub account not required). Runtime adapters for Claude Code / Custom GPT / Copilot Agent will be added under [`runtime-adapters/`](runtime-adapters/) in v0.3 and later.

---

## About, license, and contributing

**Contact:** [gmoriki.com](https://gmoriki.com) | [note (Japanese)](https://note.com/pogohopper8) | [@gmoriki](https://github.com/gmoriki)

**Disclaimer:** The content in this repository is intended for informational purposes only and does not constitute legal advice. Japan's Personal Information Protection Act and each institution's internal regulations take precedence. Final operational decisions should follow the rules and instructions of the relevant university department.

**License:** [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — see [LICENSE](LICENSE) for details.

**Related documents:** [DESIGN.md](DESIGN.md) (design philosophy) / [CONTRIBUTING.md](CONTRIBUTING.md) (contribution guide) / [CHANGELOG.md](CHANGELOG.md) (release notes) / [docs/update-policy.md](docs/update-policy.md) (update policy)
