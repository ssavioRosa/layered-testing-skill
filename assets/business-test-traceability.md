# Business Test Traceability

## Scope and sources of truth

| Item | Detail |
| --- | --- |
| Business capability | [Name from the specification] |
| Specifications | [File/link, section and revision] |
| Technical contracts | [Schema/API/event contract, section and revision, or none] |
| In scope | [Specified flows and rules] |
| Out of scope | [Explicit exclusions from the specifications] |
| Status | [Draft / reviewed] |

## Business rule coverage

| Rule ID | Specification anchor | Business rule | Scenario IDs | Mapping status | Residual gap |
| --- | --- | --- | --- | --- | --- |
| [RULE-ID] | [Exact section] | [Concise rule] | [CASE-IDs] | [Planned / implemented / blocked] | [Gap or none] |

## Technical assurance coverage

Keep technical expectations separate from business rules. Include only obligations with an identifiable contract, schema, protocol, or approved quality requirement.

| Obligation ID | Source type and anchor | Expected guarantee | Scenario IDs | Mapping status | Residual gap |
| --- | --- | --- | --- | --- | --- |
| [TECH-API-ID] | [Contract/schema, exact section and revision] | [Input, response, state or quality guarantee] | [CASE-API-IDs] | [Planned / implemented / blocked] | [Gap or none] |

## Scenario details

### [CASE-ID] — [Business outcome]

- **Obligation type and ID:** [Business rule / Technical assurance] — [RULE-ID or TECH-ID]
- **Source anchor:** [Exact specification or contract file, section and revision]
- **Why this matters:** [Business or technical risk addressed by this scenario]
- **Given:** [Relevant initial state and input class]
- **When:** [Action or event]
- **Then:** [Observable outcome and required or forbidden side effects from the source]
- **Test layer:** [Unit / component / contract / integration / end to end]
- **Quality attribute:** [Functional / contract / robustness / security / performance]
- **Layer rationale:** [Why this is the lowest layer with sufficient signal]
- **Automated test:** [Path and stable test ID, or "Not implemented"]
- **Mapping status:** [Planned / implemented / blocked]
- **Residual gap:** [Unverified boundary or "None identified"]

## Open source refinements

Keep questions here until the specification or contract is updated. Do not present them as approved obligations or covered scenarios.

| Question | Affected source and section | Decision needed | Status |
| --- | --- | --- | --- |
| [Question] | [Section] | [Precise rule to confirm] | [Open / incorporated into spec] |
