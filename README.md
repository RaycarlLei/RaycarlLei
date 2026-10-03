# Ray

I build backend systems for AI tools: durable execution, failure recovery,
deterministic controls, and evaluation. I also maintain software that works offline.

## Selected engineering

| Project | What to inspect |
|---|---|
| [tool-journal](https://github.com/RaycarlLei/tool-journal) | A TypeScript/SQLite execution journal with lease fencing, bounded retry admission, and explicit uncertainty. Start with the [failure contract](https://github.com/RaycarlLei/tool-journal/blob/v0.3.1/docs/contract.md), run the [LangGraph recovery example](https://github.com/RaycarlLei/tool-journal/tree/v0.3.1/integrations/langgraph), or inspect the [runtime experiment](https://github.com/RaycarlLei/tool-journal/blob/v0.3.1/docs/runtime-performance.md). |
| [WordAI Community](https://github.com/RaycarlLei/WordAI) | Offline vocabulary learning in Flutter and SQLite. Inspect [meaning-level progress](https://github.com/RaycarlLei/WordAI/blob/v0.1.4/lib/services/learning_repository.dart), [content-bound answer transactions](https://github.com/RaycarlLei/WordAI/blob/v0.1.4/docs/persisted-review.md), and [transactional recovery and system file export](https://github.com/RaycarlLei/WordAI/blob/v0.1.4/docs/learning-backup.md). |

A failure you can reproduce: a service commits an action, then the HTTP receipt
is lost. In tool-journal's [synthetic HTTP example](https://github.com/RaycarlLei/tool-journal/tree/v0.3.1/examples/http),
recovery with downstream idempotency makes two calls for one effect; subsequent
replay needs no service call. [Process tests and experiment controls](https://github.com/RaycarlLei/tool-journal/blob/v0.3.1/docs/experiments.md)
separate the journal's contribution from the provider's deduplication guarantee.

Provider keys can expire. A [fixed retry admission window](https://github.com/RaycarlLei/tool-journal/blob/v0.3.1/docs/retry-admission.md)
prevents new retry leases after the cutoff, while preserving a live owner's
ability to save its receipt. The [regressions](https://github.com/RaycarlLei/tool-journal/blob/v0.3.1/tests/retry-window.test.ts)
also demonstrate the limit: local admission cannot stop a delayed request from
arriving after the provider forgets its key.

## Upstream fixes

Merged:

| Pull request | Fix |
|---|---|
| [PrefectHQ/fastmcp#5140](https://github.com/PrefectHQ/fastmcp/pull/5140) | Percent-encode data-backed file names, so `#`, `%20` and other reserved characters no longer change the resource URI. Reported in [#5137](https://github.com/PrefectHQ/fastmcp/issues/5137). |
| [crewAIInc/crewAI#7506](https://github.com/crewAIInc/crewAI/pull/7506) | Route `.txt` URLs through the existing safe URL fetcher instead of checking them as local paths. Reported in [#7505](https://github.com/crewAIInc/crewAI/issues/7505). |
| [promptfoo/promptfoo#10955](https://github.com/promptfoo/promptfoo/pull/10955) | Reject webhook results without a boolean `pass`; a `{}` response previously passed both `webhook` and `not-webhook`. |
| [agno-agi/agno#10203](https://github.com/agno-agi/agno/pull/10203) | Accept already-decoded text streams in `TextReader`, which previously returned no documents. |
| [agno-agi/agno#10213](https://github.com/agno-agi/agno/pull/10213) | Continue sitemap discovery after truncated or corrupt `.xml.gz` data. |
| [HKUDS/nanobot#5793](https://github.com/HKUDS/nanobot/pull/5793) | Apply recursive `list_dir` ignore rules only below the listed root, so `/tmp/build/project` is no longer reported as empty. |

In review:

- [CopilotKit/CopilotKit#7185](https://github.com/CopilotKit/CopilotKit/pull/7185): await results from async callable action handlers in the Python SDK.
- [HKUDS/LightRAG#3979](https://github.com/HKUDS/LightRAG/pull/3979): keep token-sized segments when the recursive chunker meets no-op separators.
- [OpenPipe/ART#908](https://github.com/OpenPipe/ART/pull/908): resume SFT dataset iteration at the exact batch instead of replaying completed batches.
- [confident-ai/deepeval#3301](https://github.com/confident-ai/deepeval/pull/3301): close observed async generators when the consuming task is cancelled.
- [confident-ai/deepeval#3302](https://github.com/confident-ai/deepeval/pull/3302): preserve `asend()` on observed async generators.

Minimal reproductions for my bug reports live in [oss-reproductions](https://github.com/RaycarlLei/oss-reproductions).

## Product work

I build [TraderBear](https://trader-bear.com/), a paper-first AI trading and research
product at Awesome Bears. Its production implementation is private. tool-journal
is an independent reference implementation informed by that work, with synthetic
examples and its own tests; it is not a mirror of the product.

I care about evidence that someone else can check: runnable examples, explicit
failure boundaries, regression tests, and design decisions with their tradeoffs.
