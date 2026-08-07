# F1 Data Project

**Repository:** [malek-pixel/F1-Data-Project](https://github.com/malek-pixel/F1-Data-Project)
**Status:** Active
**Language:** Python (100%)

## Overview

F1 Data Project is a Python data pipeline and analysis toolkit for Formula 1 race results. It pulls complete race-by-race results for every season from **2000 to 2025** from a public F1 results API, stores them locally, and turns them into win-rate and constructor-performance visualizations.

The project is intentionally scoped as a full mini-pipeline — fetch, store, analyze, visualize — rather than a single script, so it mirrors how a real data-analysis workflow is structured.

## Motivation

Formula 1 is decided by fractions of a second and season-long strategic and engineering trends that aren't visible from watching individual races. I built this project to practice the kind of data work a race engineer or strategist actually does: pulling raw results data, cleaning and structuring it, and turning it into visual trends — which constructors dominate which eras, how competitive a season was, and how win rates shift over time.

It's also my entry point into combining two interests directly: motorsport and engineering/data analysis.

## Tech Stack

- **Python 3** — core language
- - **requests** — API calls to fetch race data
  - - **pandas** — data loading, cleaning, aggregation
    - - **Matplotlib** — chart generation
      - - **CSV** — local data storage format
       
        - ## Folder Structure
       
        - ```text
          F1-Data-Project/
          │
          ├── f1_fetch.py         # Pulls race results (2000–2025) from the Jolpica F1 API into results.csv
          ├── f1_utils.py         # Shared helpers: load_results(), bucket_by_decade(), etc.
          ├── plot_wins.py        # Generates and saves chart images to /output
          ├── wins_by_year.py     # Prints each season's leading constructor and win rate
          ├── wins_by_driver.py   # Aggregates and reports race wins by driver
          ├── wins_by_decade.py   # Aggregates and reports win totals by decade
          ├── results.csv         # Stored race results dataset (season, round, race, date, position, driver, constructor)
          ├── output/              # Saved chart images (.png)
          ├── .gitignore
          └── README.md
          ```

          ## Features

          - **Resumable data collection** — `f1_fetch.py` checks `results.csv` for seasons already fetched and skips them, so the pipeline can be re-run without duplicating data or re-hitting the API unnecessarily.
          - - **Season-by-season leaderboards** — `wins_by_year.py` reports each season's race count, leading constructor, and that constructor's win rate.
            - - **Driver and constructor breakdowns** — `wins_by_driver.py` and `wins_by_decade.py` aggregate wins by driver and by decade respectively.
              - - **Automated chart generation** — `plot_wins.py` produces:
                - A line chart of the leading constructor's win rate for every season from 2000–2025
                -   - Horizontal bar charts of the top 5 constructors by wins for each decade
                    - - **Clean data access layer** — `f1_utils.py` centralizes result-loading logic (`load_results()`, `bucket_by_decade()`) so analysis scripts stay short and focused.

                    ## Visualizations

                    Chart output is generated automatically by `plot_wins.py` and saved to the `output/` folder, including:

                    - `leader_win_rate_by_year.png` — leading constructor's win rate, 2000–2025
                    - - `top_constructors_{decade}s.png` — top 5 constructors by wins, per decade
                     
                      - ## Future Roadmap
                     
                      - - Extend analysis to driver championships, not just constructor win rates
                        - - Add qualifying and lap-time data alongside race results
                          - - Build an interactive dashboard on top of the existing dataset (see Future Projects)
                          - Add basic statistical modeling (e.g., win-probability trends)
                          - - Package the pipeline so seasons can be re-fetched automatically as new races complete
                           
                            - ## Lessons Learned
                           
                            - - Working with a real, occasionally inconsistent public API (handling empty responses, missing rounds, and rate limits with `time.sleep`) instead of a clean static dataset
                              - - Structuring a project so fetching, processing, and visualization are separate, reusable pieces rather than one large script
                                - - The value of making a pipeline **resumable** rather than assuming it will always run start-to-finish in one go
                                  - - How much cleaner analysis code becomes once shared logic is pulled into a utilities module (`f1_utils.py`) instead of repeated across scripts
                                   
                                    - ## Skills Demonstrated
                                   
                                    - - Python scripting and API integration
                                      - - Data cleaning and structuring with pandas
                                        - - Data visualization with Matplotlib
                                          - - Working with time-series and categorical sports data
                                          - Writing resumable, idempotent data pipelines
                                          - - Version control and project organization with Git/GitHub
                                            - 
