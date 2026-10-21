# CommonPick verification — 21 October 2026

**Local result: PASS. Planned Studio walkthrough: COMPLETED from Accepted-state screenshots.**

| Check | Observed result |
| --- | --- |
| Authored fixture tests | 74 passed in 24.17 seconds, exit code 0 |
| Pure intersection oracle | All 729 combinations of three verdicts across two members; included in one of the 74 tests |
| GenVM lint | Passed, 3 checks |
| SDK semantic validation | Passed; CommonPick, 7 public methods (4 read, 3 write) |
| Studio execution mode | Normal (Full Consensus), shown in deployment screenshot |
| Live shared result | Round 0 progressed through WAITING_FOR_NEEDS, READY and SELECTED; hall chosen |
| Deployment | Shown ACCEPTED at the address below |
| Full finalized receipts / full ballot bodies | Not supplied or independently audited |
| GitHub publication / submission | Pending |

## What was exercised

- Planned two-wallet walkthrough, waiting state, shared YES set and one-time choice.
- No common option, unresolved cases, known rejection overriding uncertainty,
  and safe common choices coexisting with unresolved alternatives.
- Three-way common choices allow either named member to select; no automatic
  tie winner or first-option privilege.
- Membership permissions, outsiders, both-needs requirement, immutable ballots,
  duplicate round keys, per-wallet namespaces, cross-round isolation and 100-round cap.
- Original full-source report, policy/round/ballot/selection hashes, and immutable
  evidence after selection. Deterministic selection uses no model calls.
- Invalid addresses, IDs, keys, option IDs and needs; bool-versus-int checks.
- Invalid JSON, duplicate keys, extra fields, invalid verdicts and reason limits.
- Bounded format retries, provider error propagation and no fabricated UNCLEAR fallback.
- Independent-validator disagreement on any of the three verdicts; source tampering;
  semantic audit rejection; malformed audit rejection; valid negative audit not retried.
- Nondeterministic closure serialization without capturing a contract storage proxy.
- A local rejection-gate harness that raises before the first ballot write.

## Limits

Models were replaced with authored fixtures. These tests check contract behavior
given those responses. They do not measure live semantic accuracy, prompt-injection
resistance, real provider availability, multi-model agreement, deployment success
or chain finality. The uncertainty/injection fixtures do not prove a model detects
the corresponding inputs. Direct SDK mode is not a network or full rollback
simulator; the explicit gate harness only tests write placement.

The fixture suite prints a default localnet configuration during startup. These
tests use `gltest.direct.VMContext`; that startup configuration is not evidence of
a local node connection or a deployed contract.

## Setup history

The first direct-mode attempt produced fixture setup errors before its SDK cache
had been prepared. It was interrupted; the partial output is retained in
`initial_setup_attempt.txt`. No complete exception trace was captured in that log.
The official pinned runtime archive downloaded by the linter was then prepared
for direct mode using `prepare_test_sdk.py`. The full subsequent run passed.

The initial linter flagged three Python ValueError raises inside contract methods.
They were changed to SDK UserError before the successful final test and lint run.
No previous project's source or tests were modified or rerun.

## Reproduction

Python 3.12.14; genlayer-test 0.29.2; genvm-linter 0.11.0; pytest 9.1.1;
cloudpickle 3.1.2; direct SDK release v0.3.0-rc7. Pinned install and preparation
commands are in README.md.

Executed from the CommonPick project directory:

```sh
python -m pytest -x -q test_commonpick.py
genvm-lint check commonpick.py
```

Full final outputs are `local_test_results.txt` and `sdk_check_results.txt`.
The SDK log reports a newer runner is available. This prototype deliberately
retains the runner in the official first-contract page checked on 21 October 2026.

Contract SHA-256:
`ec5de2882737f09b2d47604e6f481b05b2decb3c31ba70d89e095d1bdc5a8648`

Test source SHA-256:
`e207fd40adcb7b3baaaabf2275e215d66b96a47e001dbb0e8061d47bd2bd42fb`

## Hosted observations — walkthrough complete

Studio address: `0x8b6591CF732fa0d98b6d47eE832d887811aaDf74`.
The deployment screenshot at 11:25 shows ACCEPTED. Four get_round(0) screenshots
at 11:27, 11:29, 11:31 and 11:33 show Accepted-state results:

1. Round meeting created with the intended two members; neither had submitted.
2. First member: hall YES, garden YES, video NO; second member still absent.
3. Second member: hall YES, garden NO, video NO; common_options [hall], READY.
4. Second member selected hall; status SELECTED; the previous verdicts and round
   hash remained unchanged, and the selection contains both ballot hashes.

Full normalized transcriptions are in HOSTED_RESULTS.json. The policy, round and
selection hashes were reproduced from the local policy and transcribed fields.
This checks transcription consistency; it is not an independent chain query.
Full ballot bodies and their reasons were not supplied, so the individual ballot
hashes were not recomputed or compared before and after selection. Full finalized
transaction receipts and exact deployed source bytes were not independently audited.

Source and tests are unchanged from the successful local run; no tests were rerun.
No further Studio transactions or redeployment are needed for the planned demo.
