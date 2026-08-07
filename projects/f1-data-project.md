# F1 Data Project

**Repository:** [malek-pixel/F1-Data-Project](https://github.com/malek-pixel/F1-Data-Project)
**Status:** Active
**Language:** Python (100%)

## Overview

F1 Data Project is a Python data pipeline and analysis toolkit for Formula 1 race results. It pulls complete race-by-race results for every season from 2000 to 2025 from a public F1 results API, stores them locally, and turns them into win-rate and constructor-performance visualizations.

The project is intentionally scoped as a full mini-pipeline (fetch, store, analyze, visualize) rather than a single script, so it mirrors how a real data-analysis workflow is structured.

## Motivation

Formula 1 is decided by fractions of a second and season-long strategic and engineering trends that aren't visible from watching individual races. I built this project to practice the kind of data work a race engineer or strategist actually does: pulling raw results data, cleaning and structuring it, and turning it into visual trends, such as which constructors dominate which eras, how competitive a season was, and how win rates shift over time.

It's also my entry point into combining two interests directly: motorsport and engineering/data analysis.

## Tech Stack

Python 3 is the core language. The requests library handles API calls to fetch race data, pandas handles data loading, cleaning, and aggregation, Matplotlib generates charts, and results are stored locally in CSV format.

## Folder Structure

```text
F1-Data-Project/
|
|-- f1_fetch.py         Pulls race results (2000-2025) from the Jolpica F1 API into results.csv
|-- f1_utils.py         Shared helpers: load_results(), bucket_by_decade(), etc.
|-- plot_wins.py        Generates and saves chart images to /output
|-- wins_by_year.py     Prints each season's leading constructor and win rate
|-- wins_by_driver.py   Aggregates and reports race wins by driver
|-- wins_by_decade.py   Aggregates and reports win totals by decade
|-- results.csv         Stored race results dataset (season, round, race, date, position, driver, constructor)
|-- output/             Saved chart images (.png)
|-- .gitignore
|-- README.md
```

## Features

The pipeline is resumable: f1_fetch.py checks results.csv for seasons already fetched and skips them, so it can be re-run without duplicating data or re-hitting the API unnecessarily. wins_by_year.py produces season-by-season leaderboards, reporting each season's race count, leading constructor, and that constructor's win rate. wins_by_driver.py and wins_by_decade.py provide driver and constructor breakdowns, aggregating wins by driver and by decade respectively. plot_wins.py automates chart generation, producing a line chart of the leading constructor's win rate for every season from 2000 to 2025 and horizontal bar charts of the top 5 constructors by wins for each decade. f1_utils.py acts as a clean data access layer, centralizing result-loading logic such as load_results() and bucket_by_decade() so the analysis scripts stay short and focused.

## Visualizations

Chart output is generated automatically by plot_wins.py and saved to the output/ folder, including leader_win_rate_by_year.png (leading constructor's win rate, 2000-2025) and top_constructors_{decade}s.png (top 5 constructors by wins, per decade).

## Future Roadmap

Planned next steps include extending analysis to driver championships rather than just constructor win rates, adding qualifying and lap-time data alongside race results, building an interactive dashboard on top of the existing dataset (see [Future Projects](future-projects.md)), adding basic statistical modeling such as win-probability trends, and packaging the pipeline so seasons can be re-fetched automatically as new races complete.

## Lessons Learned

Working with a real, occasionally inconsistent public API, including handling empty responses, missing rounds, and rate limits with time.sleep, was different from working with a clean static dataset. Structuring the project so fetching, processing, and visualization are separate, reusable pieces rather than one large script made it easier to extend. Making the pipeline resumable rather than assuming it would always run start-to-finish in one go proved valuable in practice. Pulling shared logic into a utilities module, f1_utils.py, instead of repeating it across scripts made the analysis code noticeably cleaner.

## Skills Demonstrated

This project demonstrates Python scripting and API integration, data cleaning and structuring with pandas, data visualization with Matplotlib, working with time-series and categorical sports data, writing resumable and idempotent data pipelines, and version control and project organization with Git and GitHub.
