# Board Battles — NHL Draft Rankings, Graded

**Board Battles grades the scouts.** It aggregates NHL pre-draft rankings from
across the scouting world and scores each source on two separate skills:
predicting **where** players get drafted (*Draft Accuracy*) and predicting a
player's **long-term value** (*Value Prediction*). It also blends every board
into a consensus with a disagreement band and, where the data supports it,
movement over time.

This repository holds **only the published, self-contained static site**
(`index.html`) — a baked snapshot with no server, no database, and no sensitive
data. It is served via GitHub Pages. The source code and data pipeline live in a
separate, private repository.

## How the grades work (in brief)
Each scout board is compared to what actually happened. **Draft Accuracy**
measures how closely a board predicted the real draft order (slot error, rank
correlation, top-10 hit rate). **Value Prediction** measures how well a board
anticipated players' NHL value (Point Shares and outcome tiers), slot-relative
so credit is earned for beating the pick. Grades are presented as a band with a
confidence/coverage signal and trend — never a bare letter — and are field-
curved once enough boards exist in a class. Full method:
`docs/grading-methodology.md` in the code repo.

## Data & attribution
Every ranking belongs to the analyst or outlet that produced it, not to this
project. We measure and link back; we do not republish boards. See
[`CREDITS.md`](CREDITS.md) for full attribution to the aggregators, public
scouts/outlets, and paid sources.

**Paywalled sources** (e.g. The Athletic / Pronman & Wheeler, McKeen's,
FCHockey, Red Line Report, ISS, Hockey Prospect) are graded and counted toward
consensus but are **never reproduced**: no ordered board, no exact ranks. Public
output shows only derived measurements, coarse ranges where public coverage is
sufficient, and a link to the original. This is enforced in the build, not by
hand — the exporter recomputes every published number from non-paid boards only
and fails the build if any paid rank could surface or be reconstructed.

## Coverage
Draft outcomes + player value are loaded for **2015–2026**; scout boards for
**2016–2026** (varies by class). Some classes are outcome-only or board-only
depending on maturity and availability, and the site labels these. A couple of
draft years are not yet backfilled.

## License
The site's **code** is MIT-licensed (in the separate code repository). The
**draft-ranking data displayed here is not open-licensed** — it is credited to
its sources and, for paid sources, obfuscated. See [`LICENSE`](LICENSE).

## Status & disclaimer
Board Battles is an independent research/measurement project, not affiliated with
the NHL or any outlet graded. A human intellectual-property / media-law review is
**recommended before any wider public promotion** of this project — the
"measure, don't reproduce" posture is careful but is not a substitute for legal
sign-off.

---
### Publish / update (maintainer notes)
This site is regenerated from the private code repo with
`python3 webapp/deploy_site.py` (rebuilds the snapshot, runs the paywall safety
gate, writes `index.html`), then the `site/` folder is committed and pushed.
GitHub Pages serves from `main` / root; `.nojekyll` is included.
