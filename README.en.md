# higher-ed-ai-skills

Agent Skills for Japanese higher education staff who want to delegate university work to AI agents.

The skills help agents support academic affairs, student support, research administration, IR, public relations, international office work, committee operations, staff training, and document review while respecting university-specific rules, authority, information handling, and approval paths.

[日本語](README.md)

## What This Is

University administration depends on context that is rarely written down: committee norms, approval routes, faculty-staff authority boundaries, student data handling, academic calendars, and department-specific practice.

This repository publishes that operational knowledge as `SKILL.md` files. The direct reader is an AI agent. University staff should usually ask the agent in natural language and let it invoke the relevant skill.

## Start With Input Preflight

Before sharing document text or files, ask the agent to triage document type, intended use, likely information categories, publication scope, and AI runtime conditions.

```text
I want to summarize a faculty meeting packet.
Do not open or read the file yet.
First triage whether this can be given to an AI agent based only on document type, likely information categories, purpose, and runtime.
```

| Need | Start with | Then use |
|---|---|---|
| Check whether material can be shared with an AI agent | [check-info-level](skills/check-info-level/) | [confidential-info-guidelines](skills/confidential-info-guidelines/) |
| Classify information and input conditions | [confidential-info-guidelines](skills/confidential-info-guidelines/) | [ai-use-risk-classification](skills/ai-use-risk-classification/) |
| Decide where AI can be used in a business process | [ai-use-risk-classification](skills/ai-use-risk-classification/) | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) |

## Choose By Work

| Work | Example request | Skill | Output |
|---|---|---|---|
| Committees | Decide where AI can help with committee minutes | [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | Agenda risk, allowed use, confirmation path, workflow |
| Academic affairs | Add an AI use policy to a syllabus | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | Policy level, sample wording, student communication |
| Admissions | Write an AI use policy for application documents | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | Policy options, suspected-use process, committee checks |
| Student support | Split student inquiries into AI-answerable and human-handled cases | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | Inquiry classes, escalation rules, residual risk |
| International office | Prepare multilingual guidance for international students | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | Document type, reviewers, translation workflow |
| Research support | Answer questions about AI disclosure in papers or grants | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | Disclosure need, prohibited uses, policy checks |
| IR and quality assurance | Analyze free-text student survey responses | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | Anonymization, analysis steps, validation checks |
| PR and documents | Review public-facing copy or student notices | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/), [ai-tone-check](skills/ai-tone-check/) | Fact checks, reader load, tone edits |

## Institutional Enablement

AI governance is not the repository's main identity. It is treated as organizational enablement for doing university work responsibly.

| Need | Skill | Output |
|---|---|---|
| Define departmental or institution-wide AI use rules | [ai-use-risk-classification](skills/ai-use-risk-classification/) | Prohibited / limited / recommended / open use categories |
| Bring an AI adoption proposal to a committee or executive body | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | Maturity diagnosis, discussion points, executive memo |
| Build a staff training session | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | 30-60 minute training plan, exercise, check questions |

## Skill Authoring

Use [create-action-skill](skills/create-action-skill/) when turning local university work know-how into a new skill. Contributors should follow [AGENTS.md](AGENTS.md) and [references/skill-format-guide.md](references/skill-format-guide.md).

## Full Catalog

| Category | Skill | Version |
|---|---|---|
| Input preflight | [confidential-info-guidelines](skills/confidential-info-guidelines/) | 1.5.0 |
| Input preflight | [check-info-level](skills/check-info-level/) | 1.3.0 |
| Input preflight / enablement | [ai-use-risk-classification](skills/ai-use-risk-classification/) | 1.2.0 |
| Committees | [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | 1.2.0 |
| Document review | [ai-tone-check](skills/ai-tone-check/) | 1.2.0 |
| Institutional enablement | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | 1.2.0 |
| Institutional enablement | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | 1.2.0 |
| Skill authoring | [create-action-skill](skills/create-action-skill/) | 1.1.0 |
| Academic affairs | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | 1.3.0 |
| Admissions | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | 1.2.0 |
| Student support | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | 1.2.0 |
| International office | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | 1.2.0 |
| Research support | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | 1.3.0 |
| IR and quality assurance | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | 1.2.0 |
| Public relations | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/) | 1.2.0 |

See [docs/roadmap.md](docs/roadmap.md) for planned areas and [deprecated/](deprecated/) for retired skills.

## Install

See [docs/install.md](docs/install.md) for installation and [docs/using-with-agent.md](docs/using-with-agent.md) for request patterns.

Claude Code example:

```bash
git clone https://github.com/gmoriki/higher-ed-ai-skills.git
mkdir -p ~/.claude/skills/
cp -R higher-ed-ai-skills/skills/check-info-level \
  ~/.claude/skills/higher-ed-check-info-level
```

Use fictional data or document categories for initial testing. Do not test with real student, personnel, admissions, or unpublished research data.

## Safety And Limits

- Your institution's rules, information security policy, privacy policy, and AI use guidelines always take precedence.
- This repository is not legal advice.
- Before sharing student information, grades, advising records, personnel information, admissions material, or unpublished research data, triage input permissibility first.
- Before uploading files to external AI services, confirm contract type, training use, retention, and deletion procedures.

## License

Repository content is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
