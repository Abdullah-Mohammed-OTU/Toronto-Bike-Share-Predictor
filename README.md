# Toronto Bike Share: Winter Ridership Analysis (January 2024)

An exploratory data visualization project in R that looks at how Torontonians use Bike Share in the middle of winter. Using every trip logged in January 2024, it asks three questions: what the main trends are, when people ride, and where trips start.

## Key Findings

- **Weekdays beat weekends.** Ridership peaks in the morning and evening commute windows.
- **Commute trips are short.** Trips that start during rush hour are mostly under 10 minutes. Long trips (>30 min) make up a bigger share in the early morning.
- **Demand is concentrated downtown.** Trip origins cluster heavily in Toronto's downtown core. Only 74 of the city's 158 neighbourhoods recorded any departures.
- **The dominant trip flow is Weekday → Morning → Short.** In winter, Bike Share works mainly as a commuting tool, with some recreational use alongside it.

## Visualizations

| # | Chart | Question |
|---|-------|----------|
| 1 | Stacked bar chart | How does ridership by time of day vary across the week? |
| 2 | Pie chart | What share of all trips falls in each time period? |
| 3 | Scatter plot + LOESS smooth | Does departure hour predict trip duration? |
| 4 | Proportional stacked area chart | How does the mix of short, medium and long trips shift through the day? |
| 5 | Choropleth map (`sf`) | Which neighbourhoods generate the most departures? |
| 6 | Alluvial / Sankey diagram (`ggalluvial`) | How do trips flow from day type → time of day → trip length? |

<!-- Add screenshots here, e.g. ![Choropleth](images/choropleth.png) -->

## Methodology

- **Cleaning:** Parsed timestamps with `lubridate` and converted durations to minutes. Removed trips under 1 minute or over 3 hours, plus records with missing time or location.
- **Feature engineering:** Bucketed trips into time-of-day periods (Morning / Afternoon / Evening / Night), weekday vs. weekend, and trip-length categories (<10, 10–30, >30 min).
- **Spatial join:** Converted trip start coordinates to `sf` points and joined them to the City of Toronto neighbourhood boundaries (GeoJSON) to count departures per neighbourhood.

## Tech Stack

R · tidyverse · ggplot2 · lubridate · sf · scales · ggalluvial · ggtext · R Markdown

## Data

- [Toronto Bike Share Ridership Data](https://open.toronto.ca/dataset/bike-share-toronto-ridership-data/), City of Toronto Open Data (January 2024)
- [Neighbourhoods boundaries](https://open.toronto.ca/dataset/neighbourhoods/), City of Toronto Open Data

> The original 27 MB monthly file was trimmed by about 65% (to under 5 MB) to keep the repo lightweight. The figures reflect this subset, not the full month.

## Running It

1. Clone the repo and open `toronto_bikeshare_analysis.Rmd` in RStudio.
2. Install the dependencies:
```r
   install.packages(c("tidyverse", "lubridate", "sf", "scales", "ggalluvial", "ggtext"))
```
3. Knit the notebook. The neighbourhood boundaries download at runtime, so you'll need an internet connection.

## Screenshots
