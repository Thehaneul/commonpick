# New-project research — 21 October 2026

Recommendation: **CommonPick**, a two-member meeting-option compatibility round.
These are prototype ideas, not validated businesses or claims of original invention.

| Idea | Practical purpose | Distinction and trade-off |
| --- | --- | --- |
| CommonPick | Find options that satisfy both members' natural-language needs. | Multi-member option intersection and restricted final choice. Small, observable demo; fixed options and public needs limit use. |
| SkillSwap | Match offered skills against another person's stated need. | Reciprocal service matching, rather than assigning a request to a fixed team. Matching does not prove ability or completed service; stronger practical version needs off-chain coordination. |
| IssueMerge | Group reports describing the same problem. | Consolidates duplicate records rather than choosing who handles each one. Close GenLayer prior art and risk of merging different or recurring incidents. |

## Findings

Loomio's own documentation describes polls that accept one or more choices and
can produce a shortlist. This supports group-option coordination as a real product
category, not demand for this particular blockchain implementation. CommonPick
adds interpretation of free-text constraints and contract-enforced common-option
selection. It does not replace Loomio or claim an integration.

TimeBanks describes communities exchanging services and tracking time credits.
This supports the broad need for skill exchange. Our alternative would only match
descriptions; it would not be a time-credit system or prove a fair/performed trade.
Its additional practical coordination makes it a weaker fit for a short demo.

GenLayer-Dedup-Registry already documents semantic duplicate detection. Its README
is prior-art evidence, not an independently audited deployment or benchmark. The
search also surfaced intent-lock, which addresses semantic duplicate agent actions.
IssueMerge would need a sharper distinction before being worth building.

GenLayer's fit guide recommends a shared state consequence driven by language or
judgment, with validators able to check the input. CommonPick's consequence is
which choices its two members are permitted to record. The candidate descriptions
and each member's entire requirement are available to validators. If a trusted
organiser or conventional poll suffices, use that simpler alternative instead.

## Difference from our seven earlier projects

| Previous project | Earlier purpose | CommonPick's difference |
| --- | --- | --- |
| SourceRoots | Evidence origins and separate evidence-producing events | Does not track evidence lineage; computes shared compatibility. |
| HoldoutLedger | Documented separation of experimental groups | No experiments, dataset admission or leakage decisions. |
| ScopeHandshake | Approval of client work outside an agreed brief | No brief changes, prices or two-party change approvals; either member may select a common option under a fixed rule. |
| NoticeParity | Fidelity of translated notices and reuse permission | No translation, text equivalence or reuse authorisation. |
| ExplainGate | Learning checkpoints and advancement | No grading, lessons or learner progression. ExplainGate remains untouched. |
| SurplusHold | Stock reservations and release | No quantities, scarcity, held inventory or release action. |
| QueuePact | Routing tasks to teams and acknowledgement rights | Aggregates two members' compatible-option sets; no task assignment or team acknowledgement. |

Validation, source preservation and wallet checks are reusable engineering patterns.
The new state machine is a choice round with two independent requirement records,
a set intersection, and one permitted selection. The name CommonPick is a working
label; targeted searching did not establish an existing GenLayer project with that
name, but this is not comprehensive originality or trademark clearance.

## Planned phone scope

One deployment, one round creation, two needs submissions, one selection,
three result reads, two wallets and one wallet switch. Other rejection, uncertainty,
malformed-output and cap paths are checked locally with fixtures. Additional live
tests are not automatically required to finish this small demonstration.

## Sources checked

1. [Loomio: Choose](https://www.loomio.com/docs/en/user_manual/polls/choose)
2. [TimeBanks: How it works](https://www.timebanks.org/how-it-works)
3. [GenLayer-Dedup-Registry](https://github.com/Ritapossible/GenLayer-Dedup-Registry)
4. [intent-lock](https://github.com/nearar22/intent-lock)
5. [GenLayer: When to use GenLayer](https://docs.genlayer.com/developers/intelligent-contracts/when-to-use-genlayer)
6. [GenLayer: Equivalence Principle](https://docs.genlayer.com/developers/intelligent-contracts/equivalence-principle)
7. [GenLayer: Your first contract](https://docs.genlayer.com/developers/intelligent-contracts/first-contract)
