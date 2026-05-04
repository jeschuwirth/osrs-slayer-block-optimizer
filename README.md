# OSRS Slayer Block List Optimizer

A single-file browser tool for optimizing your Old School RuneScape slayer block list. No installs, no build step, no dependencies — just open `index.html` and go.

![OSRS Wiki aesthetic — warm parchment tones, PT Serif headings](https://img.shields.io/badge/style-OSRS%20Wiki-brown)
![Single file](https://img.shields.io/badge/build-single%20HTML%20file-green)

---

## Features

- **Monster Ratings** — Rate all 115 slayer monsters from 1 (Hate) to 4 (Love). Filter and search by name or rating tier.
- **Block Recommender** — Select a slayer master and get a ranked block list recommendation. Priority order: hated/disliked tasks first (by weight), then neutral, then loved.
- **Sortable Full Task List** — See every monster a master can assign, with live chance % recalculated against your unblocked pool. Sortable by any column.
- **Skip Analysis** — Expected net points per resolved task for three skip strategies (skip ≤1, ≤2, ≤3 rated tasks), using the geometric probability model.
- **Nieve Elite Diary toggle** — Switch Nieve between 12 and 15 base points per task depending on whether you've completed the Elite Western Provinces Diary.
- **Slayer level gating** — Monsters below your slayer level are visually dimmed and excluded from recommendations, but you can still pre-set their ratings for future planning.
- **Persistent state** — All settings, ratings, and unlocked states are saved to `localStorage` between sessions.

---

## Usage

```
git clone https://github.com/your-username/osrs-slayer-optimizer
cd osrs-slayer-optimizer
open index.html
```

No server required. Works entirely in the browser.

---

## How the Block Recommendation Works

For a given slayer master, the tool filters monsters to those the master can assign, that you meet the slayer level for, and that you've marked as unlocked. It then fills your N block slots in this priority order:

1. Monsters rated **1 (Hate)** or **2 (Dislike)**, sorted by weight descending
2. Monsters rated **3 (Neutral)**, sorted by weight descending
3. Monsters rated **4 (Love)**, sorted by weight descending

Blocking the highest-weight unwanted tasks has the most impact on your assignment pool.

## How the Skip Analysis Works

For each skip strategy, the tool computes expected net points per resolved task using a geometric series model:

```
p_skip = weight of tasks to skip / total pool weight
expected_skips = p_skip / (1 − p_skip)
net_points = base_points_per_task − (expected_skips × 30)
```

A negative result means the skip strategy costs more points than it saves on average.

---

## Data

Monster weights and slayer master pools are sourced from the [OSRS Wiki](https://oldschool.runescape.wiki) (May 2026). The dataset covers 9 slayer masters and 115 monsters.

Masters included: Turael, Spria, Mazchna, Vannaka, Chaeldar, Konar quo Maten, Krystilia, Nieve, Duradel.

> Weights are embedded directly in `index.html` as a CSV template literal. To update data, edit the `CSV` constant in the `<script>` block.

---

## Contributing

Pull requests welcome — especially for data updates as the wiki changes. The entire tool lives in one file (`index.html`), so there's no build process to worry about.

---

## License

MIT
