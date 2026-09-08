# Ray

I build backend systems for AI tools: durable execution, failure recovery,
deterministic controls, and evaluation. I also maintain software that works offline.

## Selected engineering

| Project | What to inspect |
|---|---|
| [tool-journal](https://github.com/RaycarlLei/tool-journal) | A TypeScript/SQLite execution journal with lease fencing, bounded retry admission, and explicit uncertainty. Start with the [failure contract](https://github.com/RaycarlLei/tool-journal/blob/v0.3.0/docs/contract.md), run the [LangGraph recovery example](https://github.com/RaycarlLei/tool-journal/tree/v0.3.0/integrations/langgraph), or inspect the [runtime experiment](https://github.com/RaycarlLei/tool-journal/blob/v0.3.0/docs/runtime-performance.md). |
| [WordAI Community](https://github.com/RaycarlLei/WordAI) | Offline vocabulary learning in Flutter and SQLite. Inspect [meaning-level progress](https://github.com/RaycarlLei/WordAI/blob/v0.1.3/lib/services/learning_repository.dart), [content-bound answer transactions](https://github.com/RaycarlLei/WordAI/blob/v0.1.3/docs/persisted-review.md), and [native audio ownership and failure boundaries](https://github.com/RaycarlLei/WordAI/blob/v0.1.3/docs/audio-lifecycle.md). |

A failure you can reproduce: a service commits an action, then the HTTP receipt
is lost. In tool-journal's [synthetic HTTP example](https://github.com/RaycarlLei/tool-journal/tree/v0.3.0/examples/http),
recovery with downstream idempotency makes two calls for one effect; subsequent
replay needs no service call. [Process tests and experiment controls](https://github.com/RaycarlLei/tool-journal/blob/v0.3.0/docs/experiments.md)
separate the journal's contribution from the provider's deduplication guarantee.

Provider keys can expire. A [fixed retry admission window](https://github.com/RaycarlLei/tool-journal/blob/v0.3.0/docs/retry-admission.md)
prevents new retry leases after the cutoff, while preserving a live owner's
ability to save its receipt. The [regressions](https://github.com/RaycarlLei/tool-journal/blob/v0.3.0/tests/retry-window.test.ts)
also demonstrate the limit: local admission cannot stop a delayed request from
arriving after the provider forgets its key.

## Product work

I build [TraderBear](https://trader-bear.com/), a paper-first AI trading and research
product at Awesome Bears. Its production implementation is private. tool-journal
is an independent reference implementation informed by that work, with synthetic
examples and its own tests; it is not a mirror of the product.

I care about evidence that someone else can check: runnable examples, explicit
failure boundaries, regression tests, and design decisions with their tradeoffs.
