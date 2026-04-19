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

### Cross-cutting skills (skills/)

| Skill | Description | Version |
|---|---|---|
| [confidential-info-guidelines](skills/confidential-info-guidelines/) | A three-level classification framework for deciding whether confidential information can be fed into generative AI | 1.1.0 |
| [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | AI literacy primer for new admin staff, core material for SD training | 1.0.0 |
| [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | Checklist and maturity model for institutional AI adoption reviews | 1.0.0 |
| [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | Judgment and tool-selection framework for AI-assisted meeting minutes | 1.0.0 |

### Domain-specific skills (domain-skills/)

| Domain | Skill | Description |
|---|---|---|
| [academic-affairs](domain-skills/academic-affairs/) | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | Four-level syllabus AI-policy template |
| academic-affairs | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | Admissions document AI usage and detection handling |
| [international-office](domain-skills/international-office/) | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | Multilingual communication for international students |
| [ir-analysis](domain-skills/ir-analysis/) | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | Free-form student-survey text analysis workflow |
| [public-relations](domain-skills/public-relations/) | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/) | Seven-point AI-use checklist for PR copy |
| [research-support](domain-skills/research-support/) | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | AI-use disclosure judgment for papers, theses, and grants |
| [student-support](domain-skills/student-support/) | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | AI vs human triage for student inquiries |

### Coming soon

| Skill | Note | Target |
|---|---|---|
| ai-report-evaluation | Partly absorbed by `research-integrity-ai-disclosure` and `syllabus-ai-policy` in v0.3. Standalone form re-evaluated in v0.4 | v0.4 |
| tool-selection-guide | Partly absorbed by `institutional-ai-adoption-checklist`. Standalone form re-evaluated in v0.4 | v0.4 |
| advanced-prompting-for-admin | Overlaps with `staff-ai-literacy-primer`. Merge or rename decided in v0.4 | v0.4 |
| ai-news-curation | Information-source curation | v0.5+ |
| case-library-ai-usage | Covered by expanded `case-studies/` directory | v0.5+ |

---

## Where to start

| If you are | Start here |
|---|---|
| University staff looking for practical use | [confidential-info-guidelines](skills/confidential-info-guidelines/SKILL.md) |
| Preparing an AI adoption committee | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/SKILL.md) |
| Building an SD training for new staff | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/SKILL.md) |
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
