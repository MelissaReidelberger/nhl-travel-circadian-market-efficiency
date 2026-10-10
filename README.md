# Travel, Circadian Disruption, and NHL Betting Market Efficiency

**Can an NHL team's travel schedule tell us something that the betting market has missed?**

An NHL game might begin at 7 PM in the arena, but for a team that has recently crossed several time zones, that same moment could feel quite different. Travel, limited recovery time, and demanding schedules are familiar parts of professional hockey. The harder question is whether they leave a measurable mark on performance, and whether betting markets already account for that possibility.

This project examines those questions using the 2024–25 NHL season. It combines schedule and travel reconstruction, statistical modelling, and historical betting odds to distinguish a potential performance effect from a potential market pricing error.

## The Research Question

**Are travel distance and estimated circadian disruption associated with NHL team performance, and do they provide useful information beyond what is already reflected in betting market prices?**

These are related but different questions. Even if travel affects how a team plays, that does not necessarily mean it creates a betting opportunity. A market can recognise a disadvantage and incorporate it into the odds.

## What I Found

The main result is that I did not find robust evidence that travel distance or estimated circadian disruption adds meaningful information beyond the factors already considered in the analysis or the expectations reflected in betting prices.

In the team performance models, the travel and circadian measures did not show a consistent, statistically persuasive relationship with expected goal differential, shot differential, or goal differential after accounting for team, opponent, venue, and scheduling factors.

The betting market analysis reached a similar conclusion. Across moneyline, regulation tie, and puck line markets, simulations and market adjusted regression models did not establish a reliable pattern of mispricing associated with travel or circadian disruption.

This is not proof that travel never matters, or that NHL betting markets are perfectly efficient. It means that within this season, these data, and these modelling assumptions, the analysis did not identify a dependable advantage from the travel variables studied.

That distinction matters. A useful research project should be able to report an inconclusive or negative result without turning it into a stronger claim than the evidence supports.

## How I Approached the Problem

### 1. Reconstructing Travel and Measuring Circadian Disruption

I began by connecting NHL game schedules to team locations and the sequence of games played throughout the season. From those schedules, I developed measures of travel distance, time zone changes, rest, and estimated circadian displacement.

One of the central challenges in this project was deciding how to measure circadian disruption using historical NHL data. Circadian displacement is an estimate, not a direct measurement of a player's biological clock. Because actual team travel itineraries were not consistently available, I estimated departure times using rules based on consecutive game locations, back-to-back scheduling, days between games, and time zone changes. International travel itineraries were researched separately, with documented travel times used where available.

![Travel timing decision framework](images/travel_timing_flowchart.png)


*Figure 1: Decision framework used to estimate travel timing for standard NHL scheduling scenarios. Separately researched international itineraries are not shown.*





The historical schedule, travel distance, and time zones crossed provide useful information but don't always reveal exact travel timings or how far a team's internal body clock might be from the local time at its next game.   A team that crosses several time zones and has multiple days to recover may be in a different position from one that arrives shortly before playing. This distinction is consistent with research showing that circadian adjustment following travel takes time and depends on factors beyond the number of time zones crossed (Waterhouse et al., 2007; Reilly et al., 2007). Those uncertainties informed both the feature design and the sensitivity analyses.

To account for this, I developed a schedule based estimate of residual circadian displacement. The approach reconstructs travel between consecutive game venues, estimates travel timing, and tracks a team's modelled body clock as it gradually adjusts to the surrounding time zone. Rather than resetting the body clock after every journey, the model carries its estimated state forward across the season. Research demonstrating gradual changes in circadian phase provides a physiological rationale for modelling adaptation over time rather than assuming immediate adjustment (Eastman et al., 2005).

The primary specification assumes adaptation of one hour per day when adjusting eastward and two hours per day when adjusting westward. These are modelling assumptions informed by research on jet lag and circadian adaptation, particularly evidence that adjustment can differ by travel direction (Waterhouse et al., 2007; Reilly et al., 2007). For comparison, the CDC Yellow Book describes approximate adaptation rates of one hour per day eastward and 1.5 hours per day westward (Centers for Disease Control and Prevention, 2026). I therefore also tested alternative specifications of one hour eastward and 1.5 hours westward, and one hour per day in both directions, to assess whether the results depended on the assumed adaptation rates. These sensitivity analyses examined whether the estimated relationship between circadian displacement and expected goal differential depended on the assumed adaptation rates. The findings remained statistically insignificant across all three specifications.

### 2. Testing Team Performance

The first analytical stage examined three outcomes:

1. **Expected goal differential**, a measure of the quality of scoring chances created and conceded.
2. **Shot differential**, a measure of the balance of shots for and against.
3. **Goal differential**, the difference between goals scored and allowed.

Regression models assessed how these outcomes related to travel distance and estimated circadian displacement while accounting for differences between teams and opponents, home advantage, rest, and consecutive game scheduling. This helped reduce the risk of attributing performance differences to travel when they might instead reflect team strength, opposition quality, or scheduling conditions. Standard errors were clustered by game to account for the relationship between observations from opposing teams in the same match.

I also examined whether the results depended on modelling choices, including the assumed rates of circadian adaptation and how rest and consecutive games were accounted for. The relationship between estimated circadian displacement and expected goal differential remained statistically insignificant across all three adaptation specifications. I also found no statistically significant evidence that circadian disruption had a different relationship with performance during consecutive games.

### 3. Testing Betting Market Efficiency

The second stage asked whether travel information could explain outcomes after accounting for what the betting market already expected.

The analysis covered three types of markets:

1. **Moneyline:** Which team wins the game.
2. **Regulation tie:** Whether the game is tied at the end of regulation.
3. **Puck line:** Whether a team covers a specified goal handicap, with ±1.5 as the main analysis and ±1.0 as an exploratory extension.

Two complementary approaches were used.

**Market calibration simulations** compared actual outcomes with outcomes expected from market implied probabilities. This helps distinguish an unusual observed result from the sort of variation that could occur by chance.

**Market adjusted logistic regressions** used market implied probabilities as the baseline and tested whether travel and circadian variables added explanatory information beyond that baseline. The analysis also considered different units of observation and specifications where appropriate.

The exploratory ±1.0 puck line analysis explicitly accounted for pushes, where the final result falls exactly on the handicap and the bet is neither a win nor a loss. This distinction was necessary to evaluate the market correctly rather than treating pushes as ordinary wins or losses.

## Interpreting the Results

The distinction between a performance effect and a market inefficiency is central to this project.

Suppose a team arriving from another time zone performs worse than usual. That observation alone does not imply its opponent was a good bet. If the bookmaker's price already reflects the disadvantage, there may be no pricing error to exploit.

For that reason, the analysis did not stop at identifying patterns in game results. It compared observed outcomes with market expectations and tested whether travel variables improved the explanation of those outcomes.

The results did not provide robust support for a repeatable travel based betting edge. These findings do not provide sufficient evidence to support a profitable betting strategy.

## Limitations

**One season of data.** The study focuses on the 2024–25 NHL season. A longer sample could help determine whether small effects are stable across seasons and changing team conditions.

**Estimated rather than observed circadian state.** Travel and adaptation measures are reconstructed from schedules and locations. They do not directly capture flight itineraries, sleep, individual physiology, or exact arrival times.

**Unobserved game factors.** Injuries, lineup decisions, starting goaltenders, and other changing circumstances can influence performance and are not be fully represented in the models.

**Historical market coverage.** The betting market analysis is limited to the available historical odds and eligible observations. Different markets and contract rules also produce different sample sizes. Because the analysis focuses on closing prices, it cannot establish whether markets were equally efficient when odds first became available. Initial prices may have contained discrepancies that were subsequently corrected as the market developed. Comparing opening and closing odds would therefore be a valuable extension, helping to assess how quickly travel and circadian information becomes reflected in betting prices.

**Statistical uncertainty.** A result that is not statistically persuasive is not evidence of an exact zero effect. Likewise, a suggestive individual result is not enough to establish a reliable pattern when viewed alongside the wider analysis.

## Explore the Analysis

The project is organised into three notebooks with different purposes.

| Notebook | What it contains |
| --- | --- |
| `notebooks/01_data_exploration.ipynb` | Initial data exploration and development work. |
| `notebooks/02_travel_reconstruction.ipynb` | Historical data reconstruction, travel features, and validation work. |
| `notebooks/03_final_analysis_visuals.ipynb` | The final performance models, market analyses, sensitivity checks, and visualisations. |

The final analysis uses two processed datasets:

| Dataset | Purpose |
| --- | --- |
| `data/processed/analysis_team_game_mean_final.csv` | Team performance analysis. |
| `data/processed/analysis_puckline_team_final.csv` | Puck line and related market analysis. |

For a first look at the completed research, start with `notebooks/03_final_analysis_visuals.ipynb`.

## Running the Final Notebook

The final notebook is designed to run from the `notebooks/` directory, with that directory as the working directory. It expects the two processed CSV files listed above to be present in `../data/processed/`.

The analysis uses Python, pandas, NumPy, Matplotlib, and statsmodels. Open the notebook in Jupyter, ensure the required packages are installed, and run its cells in order.

**Reproducibility note:** The final notebook starts from validated processed datasets. It does not independently retrieve all historical NHL data or repeat the full upstream reconstruction. The earlier notebooks document that development and reconstruction work. This separation keeps the final statistical analysis readable while making its data dependencies explicit.

## References

Centers for Disease Control and Prevention. (2026). *Jet lag disorder*. In *CDC Yellow Book 2026: Health information for international travel*. https://www.cdc.gov/yellow-book/hcp/travel-air-sea/jet-lag-disorder.html

Eastman, C. I., Gazda, C. J., Burgess, H. J., Crowley, S. J., & Fogg, L. F. (2005). Advancing circadian rhythms before eastward flight: A strategy to prevent or reduce jet lag. *Sleep, 28*(1), 33–44. https://doi.org/10.1093/sleep/28.1.33

Reilly, T., Waterhouse, J., & Edwards, B. (2007). Coping with jet lag: A position statement for the European College of Sport Science. *European Journal of Sport Science, 7*(1), 1–7. https://doi.org/10.1080/17461390701216823

Waterhouse, J., Reilly, T., Atkinson, G., & Edwards, B. (2007). Jet lag: Trends and coping strategies. *The Lancet, 369*(9567), 1117–1129. https://doi.org/10.1016/S0140-6736(07)60529-7
