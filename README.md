# Ray

I build backend systems for AI tools: durable execution, failure recovery,
deterministic controls, and evaluation. I also maintain software that works offline.

## Selected engineering

| Project | What to inspect |
|---|---|
| [tool-journal](https://github.com/RaycarlLei/tool-journal) | A TypeScript/SQLite execution journal with lease fencing, explicit uncertainty, and real process-crash tests. Start with the [failure contract](https://github.com/RaycarlLei/tool-journal/blob/main/docs/contract.md) or [run the experiment](https://github.com/RaycarlLei/tool-journal#try-the-failure). |
| [WordAI Community](https://github.com/RaycarlLei/WordAI) | Offline vocabulary learning in Flutter and SQLite. Explore [meaning-level progress](https://github.com/RaycarlLei/WordAI/blob/main/lib/services/learning_repository.dart), [review preparation](https://github.com/RaycarlLei/WordAI/blob/main/lib/services/review_preparation.dart), and [pronunciation tests](https://github.com/RaycarlLei/WordAI/blob/main/test/review_pronunciation_test.dart). |

A failure you can reproduce: a service commits an action, then the HTTP receipt
is lost. In tool-journal's [synthetic HTTP example](https://github.com/RaycarlLei/tool-journal/tree/v0.1.1/examples/http),
recovery with downstream idempotency makes two calls for one effect; subsequent
replay needs no service call. Without that downstream contract, recovery stays
indeterminate after lease expiry. [Regression tests](https://github.com/RaycarlLei/tool-journal/blob/v0.1.1/tests/http-recovery.test.ts)
and [experiment controls](https://github.com/RaycarlLei/tool-journal/blob/v0.1.1/docs/experiments.md)
make the distinction inspectable.

## Product work

I build [TraderBear](https://trader-bear.com/), a paper-first AI trading and research
product at Awesome Bears. Its production implementation is private. tool-journal
is an independent reference implementation informed by that work, with synthetic
examples and its own tests; it is not a mirror of the product.

I care about evidence that someone else can check: runnable examples, explicit
failure boundaries, regression tests, and design decisions with their tradeoffs.
