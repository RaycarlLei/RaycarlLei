# Ray

I build backend systems for AI tools: durable execution, failure recovery,
deterministic controls, and evaluation. I also maintain software that works offline.

## Selected engineering

| Project | What to inspect |
|---|---|
| [tool-journal](https://github.com/RaycarlLei/tool-journal) | A TypeScript/SQLite execution journal with lease fencing, explicit uncertainty, and real process-crash tests. Start with the [failure contract](https://github.com/RaycarlLei/tool-journal/blob/v0.1.2/docs/contract.md) or run the [LangGraph recovery example](https://github.com/RaycarlLei/tool-journal/tree/v0.1.2/integrations/langgraph). |
| [WordAI Community](https://github.com/RaycarlLei/WordAI) | Offline vocabulary learning in Flutter and SQLite. Inspect [meaning-level progress and import transactions](https://github.com/RaycarlLei/WordAI/blob/v0.1.1/lib/services/learning_repository.dart), [import failure regressions](https://github.com/RaycarlLei/WordAI/blob/v0.1.1/test/home_import_widget_test.dart), and [bounded speech downloads](https://github.com/RaycarlLei/WordAI/blob/v0.1.1/test/community_gateway_test.dart). |

A failure you can reproduce: a service commits an action, then the HTTP receipt
is lost. In tool-journal's [synthetic HTTP example](https://github.com/RaycarlLei/tool-journal/tree/v0.1.2/examples/http),
recovery with downstream idempotency makes two calls for one effect; subsequent
replay needs no service call. Without that downstream contract, recovery stays
indeterminate after lease expiry. [Regression tests](https://github.com/RaycarlLei/tool-journal/blob/v0.1.2/tests/http-recovery.test.ts)
and [experiment controls](https://github.com/RaycarlLei/tool-journal/blob/v0.1.2/docs/experiments.md)
make the distinction inspectable.

The [LangGraph process tests](https://github.com/RaycarlLei/tool-journal/blob/v0.1.2/integrations/langgraph/tests/recovery.test.ts)
also kill a node after the journal saves its receipt but before the graph records
the node's result. Resuming from the official SQLite checkpoint retrieves that
receipt without another HTTP call.

## Product work

I build [TraderBear](https://trader-bear.com/), a paper-first AI trading and research
product at Awesome Bears. Its production implementation is private. tool-journal
is an independent reference implementation informed by that work, with synthetic
examples and its own tests; it is not a mirror of the product.

I care about evidence that someone else can check: runnable examples, explicit
failure boundaries, regression tests, and design decisions with their tradeoffs.
