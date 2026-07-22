# MLS Elo Ratings Dataset

Historical and up-to-date Elo ratings for Major League Soccer (MLS), covering every regular-season and playoff match from the league's inaugural 1996 season to the present.

### Context

This project is inspired by [ClubElo](http://clubelo.com/), which has long provided Elo ratings for major European football leagues. No equivalent dataset existed for MLS, so I built one myself. It is also part of [oddsline.io](https://oddsline.io), a football betting analytics platform I develop and operate as a solo founder — this repository is the public, source-of-truth home for the underlying MLS Elo data.

### Content

- `results.csv` — every included MLS match, with pre-match and post-match Elo ratings for both teams
- `teams.csv` — each team's current Elo rating and when it was last updated
- `home_advantage.csv` — the current home-field advantage parameter used in the model

`results.csv` columns:

- `date` — match date (`YYYY-MM-DD`)
- `home_team` / `away_team` — team names (current naming used throughout)
- `home_elo_current` / `away_elo_current` — each team's Elo rating going into the match
- `home_score` / `away_score` — full-time score
- `result` — match outcome from the home team's perspective (`H`/`D`/`A`)
- `neutral` — whether the match was played at a neutral venue
- `home_elo_update` / `away_elo_update` — each team's Elo rating after the match

`teams.csv` columns:

- `team` — team name
- `elo` — current Elo rating
- `last_updated_date` — date this rating was last recalculated

`home_advantage.csv` columns:

- `home_advantage` — current home-field advantage value used in the model
- `last_updated_date` — date this value was last recalculated

**Note on team names**: Team names are unified to each club's *current* name throughout the dataset, including for historical matches. For example, matches played by the "MetroStars" in the 1990s are listed under the team's current name, New York Red Bulls. This is done so a team's full history and stats can be tracked under a single, consistent name.

### Methodology

The model follows the standard Elo methodology used across most football Elo implementations:

- **Scope**: Only MLS league matches are included — from the first MLS match in 1996 through the most recent match played. Cup competitions (e.g., U.S. Open Cup, Leagues Cup) and continental competitions (e.g., CONCACAF Champions Cup) are **not** included.
- **Initial rating**: Every team starts at an Elo of **1,500**.
- **Match weighting**: All matches are weighted equally — there is no additional weight for playoffs, rivalries, or other match types.
- **Margin of victory**: The Elo update accounts for goal difference — a team that wins by a larger margin gains more Elo than a team that wins narrowly.
- **Everything else** (expected score calculation, 400-point ratings scale, home-field advantage adjustment, etc.) follows conventional Elo methodology.
- **Two-legged playoff rounds (2003–2018)**: Some Conference Semifinals/Finals during this period were decided over two legs (aggregate score). For these ties, the two legs are combined into a single aggregate result and treated as one neutral-site match for Elo purposes, rather than as two separate updates.
- **Extra time**: Some historical playoff matches may include extra-time scores. Going forward, updates will only use the regulation-time (90-minute) score.

Data compiled from publicly available match results.

### Updates

Elo ratings are updated manually after MLS match days, on a best-effort basis, so this dataset should stay current within a few days of each round of matches.

### License

Copyright (c) 2026 Philo Park.

This dataset is licensed under [CC BY 4.0](LICENSE). The license applies to the calculated Elo ratings and home-field advantage values (the `home_elo_current`, `away_elo_current`, `home_elo_update`, `away_elo_update`, and `elo` columns, and `home_advantage.csv`) — the underlying match facts (dates, teams, scores) are not subject to copyright. See [LICENSE](LICENSE) for the full license text.

### Citation

If you use this dataset, please cite it — see [CITATION.cff](CITATION.cff), or use the "Cite this repository" button on GitHub.

### Contribute

If you notice an error or a missing/incorrect match result, feel free to open an issue or submit a pull request.
