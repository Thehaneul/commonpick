# CommonPick

Find a meeting format that fits two people's stated needs, then record a choice
that is compatible with both. Built as a GenLayer Intelligent Contract.

**Version:** `commonpick-0.1`. **Status:** planned Studio walkthrough completed
on 21 October 2026, evidenced by user-supplied Accepted-state screenshots.

**Studio address:** `0x8b6591CF732fa0d98b6d47eE832d887811aaDf74`

Round 0 reached `SELECTED` with `hall`, selected by the second member.
See `HOSTED_RESULTS.json` for the transcribed observations and `VERIFICATION.md`
for local checks and evidence limits. GitHub publication and submission are pending.

## A simple example

One member wants to meet in person. The other needs a seated indoor activity.
The contract compares their needs with three fixed descriptions:

| Option ID | Meeting format | First member | Second member |
| --- | --- | --- | --- |
| `hall` | Seated indoor board games, in person | YES | YES |
| `garden` | An outdoor walk, in person | YES | NO |
| `video` | A remote video conversation | NO | NO |

These verdicts were observed in the Studio walkthrough. The example needs above
come from the guided inputs; full stored ballot texts/reasons were not supplied.
The common set is `hall`. Either named member may select it. The contract will
reject a garden or video selection, and retain both original assessments.

## How it works

1. Anyone creates a round naming their own wallet and one different partner wallet.
2. Each member submits their own short needs statement once.
3. GenLayer validators independently assess each option as YES, NO or UNCLEAR,
   compare all three verdicts, and audit the proposed explanation.
4. Deterministic code computes the intersection of the YES sets.
5. Either member can select one option in that intersection, once. There is no
   automatic first-option winner or preference ranking.

The three option descriptions and interpretation rules are fixed in this version.
No organiser can replace a member, edit a ballot, reinterpret saved needs, or
select on behalf of someone else's round. Public reads remain available.

## Why GenLayer

The judgment is whether an ordinary-language requirement is compatible with a
description. Its agreed result determines the options the contract permits the
two wallets to select. Neither a frontend-supplied verdict nor one operator's
model response can directly set that permission.

This is a conditional fit for parties who want a shared decision rule and record.
A normal poll or database is simpler when participants can directly tick their
acceptable options and trust the organiser. Customer demand is not established.

## Status meanings

| Status | Meaning |
| --- | --- |
| WAITING_FOR_NEEDS | One or both members have not submitted. |
| READY | At least one option is YES for both; members can select it. |
| REVIEW_REQUIRED | No common YES yet; at least one option is unresolved without a definite NO. |
| NO_COMMON_OPTION | Every option has a definite NO from at least one member. |
| SELECTED | One common option has been recorded; further selection is blocked. |

A READY round may also have unresolved alternatives. Those alternatives cannot be
selected. A definite NO from either member excludes an option even if the other
member's verdict is UNCLEAR. A malformed model response is an execution error,
not a saved UNCLEAR ballot. REVIEW_REQUIRED has no manual override in this version;
create a fresh round with clearer requirements to reassess.

## Contract API

Constructor: no inputs.

| Method | Type | Inputs |
| --- | --- | --- |
| `get_rules` | Read | None |
| `get_round` | Read | `round_id` (integer) |
| `get_ballot` | Read | `round_id`, `member_index` (0 = creator; 1 = partner) |
| `get_round_id` | Read | `creator` (full wallet), `round_key` |
| `create_round` | Write | `round_key`, `partner_wallet` |
| `submit_needs` | Write | `round_id`, `requirements` |
| `select_option` | Write | `round_id`, `option_id` (`hall`, `garden` or `video`) |

Round IDs start at 0. Keys are per creator wallet, max 40 lowercase letters,
digits, underscores or hyphens. Requirements are 1–600 characters and cannot be
blank. There are at most 100 rounds per instance. `get_round_id` returns -1 if
the key is not saved. The constructor requires no second wallet; the partner is
chosen later when creating a round.

## Evidence and boundaries

- Sources are attached by code rather than quoted back by a model.
- Round hashes bind members, round key, version and policy hash. Ballot hashes
  bind each member and their full saved assessment to that round.
- The final selection hash binds the selected option, selecting wallet and both
  original ballot hashes. Hashes show record consistency, not factual truth.
- Membership is by wallet, not verified person. One person can control both
  wallets in a demo. Two wallets are not proof of two independent people.
- Needs and assessments are public. Use fictional, non-sensitive demo needs.
- This checks stated descriptions only. No venue facts, availability, access
  requirements, weather or safety are independently verified.
- Selection is a plan record: no booking, payment, notifications, reservation,
  proof of attendance or further confirmation by both members occurs.
- Either member may choose among the shared YES options; submitting needs uses
  this explicit selection rule. This is not a majority vote or joint signature.
- English only, three fixed meeting formats, two named wallets, immutable ballots.
  There is no cancellation, amendment, time limit, private ballot or group expansion.
- AI/provider/consensus failures remain possible. Local fixture tests cannot
  establish live model accuracy, prompt-injection resistance or network finality.

## Local development

Use Python 3.12. Create a virtual environment, then:

```sh
python -m pip install -r requirements-dev.txt
python prepare_test_sdk.py
python -m pytest -x -q test_commonpick.py
genvm-lint check commonpick.py
```

The prep script obtains the official pinned SDK archive and makes it available to
both local tools. It may download a runtime release on first use. The contract's
runner identifier follows the official first-contract documentation checked
21 October 2026. The linter's newer-runner notice is retained in the check log.

## Phone and GitHub

The planned walkthrough is complete; do not repeat its transactions.
`PHONE_WALKTHROUGH.txt` is retained as the original reproduction procedure.
For a separate future reproduction, the contract file is **only `commonpick.py`**;
the other Python files are tests or setup tooling.

The delivery ZIP is flat: extract it once into a new folder and upload the files
to a new `commonpick` repository. There is no nested old version to overwrite the
current source. Submission copy is in `GITHUB_AND_SUBMISSION.txt`; the deployed
address is filled in. Add the actual repo URL after upload verification. No
submission has been reported.
