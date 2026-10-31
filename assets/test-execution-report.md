# Test Execution Report

## Executive summary

| Item | Result |
| --- | --- |
| Business capability | [Name] |
| Specification revision | [Revision/link] |
| Technical contract revision | [Schema/API/event contract revision/link, or none] |
| Code revision | [Commit/version] |
| Environment | [Controlled environment and relevant configuration] |
| Test stack | [Tools and versions] |
| Commands | [Commands actually run] |
| Overall assessment | [Verified / failed / blocked, with a short reason] |

## Three-run stability check

| Run | Started at | Duration | Passed | Failed | Skipped | Blocked | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | [Time] | [Duration] | [Count] | [Count] | [Count] | [Count] | [Log/report] |
| 2 | [Time] | [Duration] | [Count] | [Count] | [Count] | [Count] | [Log/report] |
| 3 | [Time] | [Duration] | [Count] | [Count] | [Count] | [Count] | [Log/report] |

## Business rule coverage

| Specified rules | Mapped | Implemented | Verified in all required runs | Gaps |
| --- | --- | --- | --- | --- |
| [Count] | [Count] | [Count] | [Count] | [Rule IDs] |

## Technical assurance coverage

| Contract obligations | Mapped | Implemented | Verified in all required runs | Gaps |
| --- | --- | --- | --- | --- |
| [Count] | [Count] | [Count] | [Count] | [Technical obligation IDs] |

## Scenario results

| Scenario ID | Obligation type | Layer | Run 1 | Run 2 | Run 3 | Duration by run | Evidence | Finding and next action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [CASE-ID] | [Business rule / Technical assurance] | [Layer] | [Pass/fail/skipped/blocked/not run] | [Status] | [Status] | [Durations] | [Link] | [Observed failure or none] |

## Performance and robustness

| Requirement or baseline | Workload/fault model | Measure | Target from spec | Observed | Assessment |
| --- | --- | --- | --- | --- | --- |
| [Spec anchor or "Observed baseline"] | [Profile] | [p95, throughput, error rate, recovery, suite duration, etc.] | [Specified target or "No target specified"] | [Measured result] | [Meets target / regression / baseline only / blocked] |

## Mutation effectiveness

| Rule/scenario ID | Mutation and code location | Expected detecting test | Outcome | Evidence | Follow-up |
| --- | --- | --- | --- | --- | --- |
| [ID] | [Removed operation / changed condition or value] | [Test ID] | [Killed/survived/no coverage/invalid/equivalent/not run] | [Report] | [Action] |

Mutation score: [Detected / valid mutants, with exclusions and tool definition]. A high score is evidence of test sensitivity, not proof of complete correctness.

## Outstanding gaps

| Gap | Business impact | Owner or next decision | Evidence needed |
| --- | --- | --- | --- |
| [Gap] | [Impact] | [Action] | [Required evidence] |
