# Ray

I build backend systems for AI tools: durable execution, failure recovery,
deterministic controls, and evaluation. I also maintain software that works offline.

## Selected engineering

| Project | What to inspect |
|---|---|
| [tool-journal](https://github.com/RaycarlLei/tool-journal) | A TypeScript/SQLite execution journal with lease fencing, explicit uncertainty, and real process-crash tests. Start with the [failure contract](https://github.com/RaycarlLei/tool-journal/blob/main/docs/contract.md) or [run the experiment](https://github.com/RaycarlLei/tool-journal#try-the-failure). |
| [WordAI Community](https://github.com/RaycarlLei/WordAI) | Offline vocabulary learning in Flutter and SQLite. Explore [meaning-level progress](https://github.com/RaycarlLei/WordAI/blob/main/lib/services/learning_repository.dart), [review preparation](https://github.com/RaycarlLei/WordAI/blob/main/lib/services/review_preparation.dart), and [pronunciation tests](https://github.com/RaycarlLei/WordAI/blob/main/test/review_pronunciation_test.dart). |

## Product work

I build [TraderBear](https://trader-bear.com/), a paper-first AI trading and research
product at Awesome Bears. Its production implementation is private. tool-journal
is an independent reference implementation informed by that work, with synthetic
examples and its own tests; it is not a mirror of the product.

I care about evidence that someone else can check: runnable examples, explicit
failure boundaries, regression tests, and design decisions with their tradeoffs.
