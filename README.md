# Layered Testing Skill

A reusable Agent Skill for **Codex and Claude** focused on spec-led test planning, implementation, and execution feedback. It maps business rules to the lowest test layer that gives a reliable signal, then records what was actually verified.

Uma skill para mapear regras de negócio a partir das specs, escolher a stack de testes conforme a aplicação e criar uma suíte rápida com rastreabilidade legível em inglês.

## What it does

- Inspects the application's language, architecture, test setup, interfaces, and CI before choosing tools.
- Maps each specified rule and relevant variation to unit, component, contract, integration, or a small number of end-to-end tests.
- Keeps a business-readable traceability map and execution report in English, with stable rule and scenario IDs.
- Runs the relevant suite three times and records each outcome to expose instability.
- Checks robustness, application performance, suite duration, and mutation effectiveness where the specification and project support them.
- Reports gaps and residual risk. A high coverage or mutation score does not prove complete correctness.

```mermaid
flowchart LR
  A[Business specifications] --> B[Rules and scenario IDs]
  B --> C[Smallest reliable test layer]
  C --> D[Three verified runs]
  C --> E[Robustness, performance and mutation]
  D --> F[English execution report]
  E --> F
```

## Install and use in Codex

Clone the repository into your user skills directory:

```bash
git clone https://github.com/ssavioRosa/layered-testing-skill.git ~/.codex/skills/testes-por-camadas
```

Or download the versioned ZIP from [Releases](https://github.com/ssavioRosa/layered-testing-skill/releases) and extract the `testes-por-camadas` folder into your skills directory. The folder must contain `SKILL.md` at its root. In a repository with business specifications, invoke `$testes-por-camadas` and describe the flow to test.

## Install and use in Claude Code

For a personal skill available in all local Claude Code projects, clone this repository into Claude Code's personal skills directory:

```bash
git clone https://github.com/ssavioRosa/layered-testing-skill.git ~/.claude/skills/testes-por-camadas
```

Open Claude Code in the application repository and invoke the skill with `/testes-por-camadas`, followed by the task. Claude can also load it automatically when a request matches its description. To share the skill only within one application repository, place the extracted `testes-por-camadas` folder at `.claude/skills/testes-por-camadas/` and commit it there. The [`SKILL.md` format and these locations](https://code.claude.com/docs/en/skills) are supported by Claude Code.

## Install and use in Claude chat or Cowork

1. Download the latest `layered-testing-skill-v*.zip` from [Releases](https://github.com/ssavioRosa/layered-testing-skill/releases). Keep the ZIP intact; it contains the `testes-por-camadas` skill folder.
2. In Claude, enable **Code execution and file creation** (the newer settings may call this **Create and edit files**). Open **Customize > Skills** and choose **+ > Create skill > Upload a skill**. In the newer interface, **Customize** may appear as **Plugins**. Upload the ZIP and enable the skill.
3. Attach or provide access to the application repository and its business specifications. Ask Claude to use the `testes-por-camadas` skill for a specific flow, with the request shown below.

See Anthropic's [skill upload guide](https://support.claude.com/en/articles/12512180-use-skills-in-claude) and [interface rollout note](https://support.claude.com/en/articles/17740565-manage-plugins-skills-and-connectors-from-one-plugins-page). Claude chat and Cowork use the uploaded skill; local folders under `~/.claude/skills/` are for local Claude Code sessions and are [not read by cloud sessions](https://code.claude.com/docs/en/skills).

## Example requests

Codex:

> Use `$testes-por-camadas` to map and implement tests for the checkout flow in `specs/checkout.md`. Choose the test tools from this repository, generate English business traceability, run the relevant suite three times, and report mutation, robustness, performance, and remaining gaps.

Claude Code:

> `/testes-por-camadas` Map and implement tests for the checkout flow in `specs/checkout.md`. Generate English business traceability, run the relevant suite three times, and report mutation, robustness, performance, and remaining gaps.

Claude chat or Cowork:

> Use the `testes-por-camadas` skill to map and implement tests for the checkout flow in `specs/checkout.md`. Use the specification as the source of truth, generate English business traceability, run the relevant suite three times, and report mutation, robustness, performance, and remaining gaps.

## Files

| File | Purpose |
| --- | --- |
| [`SKILL.md`](SKILL.md) | Entry point and decision rules |
| [`references/decomposicao.md`](references/decomposicao.md) | How to assign scenarios to layers |
| [`references/registro-e-feedback.md`](references/registro-e-feedback.md) | Traceability and execution reporting |
| [`references/qualidade-da-suite.md`](references/qualidade-da-suite.md) | Stability, robustness, performance, and mutation |
| [`assets/business-test-traceability.md`](assets/business-test-traceability.md) | English traceability template |
| [`assets/test-execution-report.md`](assets/test-execution-report.md) | English execution report template |

The skill contains no application-specific business rules. It uses the target project's specs as the source of truth and asks for refinements when the expected behavior is unclear. It does not run a particular test framework or include an executable test script; those are selected and implemented for each application.

## License

MIT — see [LICENSE](LICENSE).
