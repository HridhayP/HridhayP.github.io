---
name: Bigfoot Sightings (BFRO)
tools: [Python, Altair, vega-lite]
image: /assets/pngs/bfro_map.png
description: HW5 - two Altair plots of the BFRO Bigfoot reports dataset
---

# Bigfoot Sightings (BFRO)

<div class="left">
<a class="m-1 btn btn-outline-primary btn-2 " href="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv">
  The Data
</a>
</div>
<div class="right">
<a class="m-1 btn btn-outline-primary btn-2 " href="https://github.com/HridhayP/HridhayP.github.io/blob/main/python_notebooks/hw5_bfro.ipynb">
  The Analysis
</a>
</div>

For this homework I used the BFRO Bigfoot reports dataset (4,747 reports).

## Plot 1: Map of sightings + timeline

<vegachart schema-url="/assets/json/bfro_map.json" style="width: 100%"></vegachart>

The top part is a map of where each sighting was reported, and the bottom part is a bar chart of how many reports there were each year. On the map, longitude and latitude are both quantitative and I used the albersUsa projection so Alaska and Hawaii show up. The dots are colored by classification, which is nominal (Class A is a clear sighting, Class B is something heard or seen from far away, Class C is secondhand). I used the Dark2 color scheme since it's a categorical scheme and the three colors are easy to tell apart. For the timeline, year is quantitative and binned by 1 year, and the bar height is the count of reports.

For the data, I converted the date column to a datetime and pulled out the year. I dropped rows with no latitude/longitude or date, and only kept reports from 1950 on because a few really old reports made the timeline hard to read. That left 3,780 reports. I also dropped one Washington report with a longitude of -167, which put it in the ocean, so it was probably a typo. I only kept the columns I needed so the json file wasn't huge.

## Plot 2: Top 15 states by season

<vegachart schema-url="/assets/json/bfro_states.json" style="width: 100%"></vegachart>

This is a stacked bar chart of the 15 states with the most reports, split up by season. State is nominal on the y axis, sorted by total reports. The x axis is the sum of reports, which is quantitative. Season is nominal and is the color. I picked colors that match the seasons (blue for winter, green for spring, orange for summer, brown for fall) so it's easy to read without looking at the legend much. Washington has by far the most reports (553), then California (397) and Florida (283). Most states have the most reports in summer or fall, which makes sense since that's when people are outside camping and hiking more.

For the data, I used all the reports here since this plot doesn't need coordinates. I removed reports where the season was "Unknown", then used a groupby to count reports for each state and season, and kept the top 15 states.

## Interactivity

The interactivity is in Plot 1. You can click and drag on the timeline to select a range of years and the map will only show reports from those years. You can also click a class in the legend to only show that class (shift click to pick more than one), and the timeline updates to match. I added this because the map by itself only shows where sightings happened, and with the brush you can also see when they happened. For example, if you select the early 2000s you can see the jump in reports around 2004 was spread out across the whole country.
