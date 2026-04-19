# higher-ed-ai-skills

Open-source AI skills for higher education administration, structured as skill.md files.

[日本語](README.md)

---

## What is this?

Between Japanese university operations and generative AI, translation is often required.

Universities carry a large body of undocumented tacit knowledge.

- How proposals are moved through committees
- Exceptions in the academic calendar
- Separation of authority between faculty and staff
- The quiet protocols of meeting governance

This knowledge does not transfer naturally to AI prompts. This repository publishes decision frameworks built from real higher ed work, packaged as `skill.md` files that anyone can reuse.

---

## Available skills

### Ready to use

| Skill | Description | Version |
|---|---|---|
| [**confidential-info-guidelines**](skills/confidential-info-guidelines/) | A three-level classification framework for deciding whether confidential information can be fed into generative AI | 1.1.0 |

### Coming soon

| Skill | Description | Target |
|---|---|---|
| ai-report-evaluation | Evaluation criteria and verification steps for AI-generated reports | v0.3 |
| tool-selection-guide | An AI tool selection checklist for university operations | v0.3 |
| advanced-prompting-for-admin | Applied prompt library for administrative work | v0.4 |
| ai-news-curation | Curation methods for the higher ed × AI information landscape | v0.4 |
| case-library-ai-usage | Library of AI adoption cases from other universities | v0.5 |

### Domain-specific skills

Directories are reserved under [`domain-skills/`](domain-skills/) for each department. Content will be published from v0.3 onward.

- [academic-affairs](domain-skills/academic-affairs/)
- [international-office](domain-skills/international-office/)
- [ir-analysis](domain-skills/ir-analysis/)
- [public-relations](domain-skills/public-relations/)
- [research-support](domain-skills/research-support/)
- [student-support](domain-skills/student-support/)

---

## Where to start

| If you are | Start here |
|---|---|
| University staff looking for practical use | [confidential-info-guidelines](skills/confidential-info-guidelines/SKILL.md) |
| A consultant or researcher | [DESIGN.md](DESIGN.md) |
| A Japanese reader | [README.md](README.md) |
| New to GitHub | [docs/how-to-use.md](docs/how-to-use.md) |

---

## How to use

There are three common ways to use these skills.

1. **Read them directly** — open `SKILL.md` and follow the decision flow in real-world judgment calls
2. **Feed them into an AI assistant** — paste as a system prompt or knowledge file in Claude, ChatGPT, or Microsoft Copilot
3. **Adapt them into training materials** — remix freely under CC BY-SA 4.0

See [docs/how-to-use.md](docs/how-to-use.md) for details. No GitHub account is required.

---

## License and disclaimer

All content in this repository is freely usable under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). When you redistribute adaptations, share them under the same license.

This repository is provided for informational purposes only and does not constitute legal advice. For operational decisions, follow the rules and instructions of your institution.

---

## Related documents

- [DESIGN.md](DESIGN.md) — Design philosophy and the five principles
- [CONTRIBUTING.md](CONTRIBUTING.md) — Contribution guidelines
- [CHANGELOG.md](CHANGELOG.md) — Release history
- [docs/update-policy.md](docs/update-policy.md) — Skill update policy

---

## Author

Ginga Moriki

Works at the intersection of higher education administration and AI adoption in Japan. Delivers staff training, supports institutional policy drafting, and advises on AI implementation.

The content of this repository is free to use. Paid advisory services — adapting the frameworks to specific governance structures, running training programs — are offered separately.

- [gmoriki.com](https://gmoriki.com)
- [note (Japanese)](https://note.com/pogohopper8)
- [GitHub](https://github.com/gmoriki)
