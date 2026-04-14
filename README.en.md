# higher-ed-ai-skills

Open-source AI skills for higher education administration, structured as skill.md files.

**Japanese version: [README.md](README.md)**

---

## What is this repository?

This repository provides a collection of structured, reusable AI skills tailored to higher education administration. Each skill is packaged as a `skill.md` file -- a self-contained document that defines a specific AI-augmented workflow, including context, decision frameworks, prompts, and references.

The skills address real operational challenges in university settings: handling confidential information when using AI tools, evaluating AI-generated reports, selecting appropriate AI services for institutional use, and more.

---

## Who is Ginga Moriki?

Ginga Moriki works at the intersection of higher education administration and AI adoption in Japan. He translates between the operational realities of university staff and the capabilities of modern AI systems -- designing practical frameworks, delivering training programs, and publishing tools that help institutions move from policy to practice.

- Web: <https://gmoriki.com>
- note (Japanese): <https://note.com/pogohopper8>
- GitHub: <https://github.com/gmoriki>

---

## Repository structure

```
higher-ed-ai-skills/
├── skills/                      # Cross-functional skills
│   ├── confidential-info-guidelines/
│   ├── ai-report-evaluation/
│   ├── ai-news-curation/
│   ├── advanced-prompting-for-admin/
│   ├── case-library-ai-usage/
│   └── tool-selection-guide/
├── domain-skills/               # Department-specific skills
│   ├── academic-affairs/
│   ├── international-office/
│   ├── ir-analysis/
│   ├── public-relations/
│   ├── research-support/
│   └── student-support/
├── runtime-adapters/            # Execution adapters for different AI environments
├── docs/                        # Usage guides and operational policies
├── awesome/                     # Curated AI tool lists
├── case-studies/                # Adoption case study templates
├── DESIGN.md                    # skill.md design principles
├── CONTRIBUTING.md              # Contribution guidelines
├── CHANGELOG.md                 # Release history
└── LICENSE                      # CC BY-SA 4.0
```

---

## How to use skills

Each skill lives in its own directory under `skills/` or `domain-skills/`. A skill directory typically contains:

- **SKILL.md** -- the main skill file, ready to use as-is or to feed into an AI assistant
- **examples/** -- sample inputs and outputs demonstrating the skill in action
- **references/** -- supporting materials, data tables, or external resource summaries

To use a skill:

1. Read the `SKILL.md` to understand the framework and decision logic.
2. Apply it directly to your workflow, or paste it into your AI assistant as a system prompt or reference document.
3. Adapt the examples to your institution's context.

See [DESIGN.md](DESIGN.md) for the design principles behind the skill.md format.

---

## Open vs. Premium tiers

This repository is the **open edition** of the AI skill library that Ginga Moriki has developed through work in the higher education and AI space. The principles, decision frameworks, and design philosophy published here are fully usable as-is.

For institutions that need help applying these frameworks to their specific governance structures -- such as drafting internal proposals, adapting skills to institutional decision-making processes, or running staff training programs -- Moriki offers paid consulting and advisory services. Visit <https://gmoriki.com> for details.

---

## Contributing

Contributions are welcome. Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Areas where contributions are especially valuable:

- Translations of existing skills into other languages
- Case studies from institutions that have applied these frameworks
- Corrections or updates to AI service policy comparisons in reference materials
- New domain-specific skills for underrepresented administrative areas

---

## License

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

You are free to share and adapt the material for any purpose, including commercial use, as long as you give appropriate credit and distribute derivative works under the same license.

See [LICENSE](LICENSE) for the full text.
