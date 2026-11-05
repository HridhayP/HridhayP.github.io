---
name: Where (and When) People See Bigfoot
tools: [Python, Altair, vega-lite]
image: /assets/pngs/bfro_map.png
description: Interactive map and timeline of BFRO Bigfoot sighting reports, plus a state-by-season breakdown.
---

# Where (and When) People See Bigfoot

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

This project looks at sighting reports collected by the Bigfoot Field Researchers Organization (BFRO), using the fall 2022 IS 445 copy of the dataset (4,747 reports).

## Plot 1: Sightings across the US over time (interactive)

<vegachart schema-url="/assets/json/bfro_map.json" style="width: 100%"></vegachart>

This plot shows where Bigfoot reports happened and when. The top panel is a map of every report that has coordinates and a date, from 1950 onward (3,780 reports). Each point sits at its `longitude` and `latitude`, which are both quantitative encodings, drawn on an Albers USA projection so that Alaska and Hawaii fit on the map. Points are colored by `classification`, a nominal encoding. Class A reports are clear sightings, Class B reports are things heard or glimpsed at a distance, and Class C reports are secondhand. I used the Dark2 categorical scheme because it is colorblind-friendly and gives each class a clearly different hue. The states are a light gray background so that the points stand out. The bottom panel is a bar chart of reports per year: `year` is a quantitative field binned into one-year bins, and the bar height is a quantitative `count()`.

For the data transformations, I parsed the `date` column into a datetime and extracted `year`. I dropped about 950 reports with no coordinates or date, and I dropped reports from before 1950, because a few 1800s reports stretched the timeline and made the years with most of the reports hard to read. I also removed one Washington report whose longitude (-167) put it in the middle of the Pacific Ocean, which is clearly a data-entry error. Finally, I kept only the columns the plots use and dropped the long free-text report columns, which keeps the embedded data small enough to load quickly on this page.

## Plot 2: Top states by season

<vegachart schema-url="/assets/json/bfro_states.json" style="width: 100%"></vegachart>

This plot shows the 15 states with the most reports, with each bar split by the season of the sighting. `state` is a nominal encoding on the y-axis, sorted by total reports so the ranking reads from top to bottom. The x-axis is the quantitative sum of reports. `season` is a nominal color encoding, and I chose colors that people already associate with the seasons (blue for winter, green for spring, orange for summer, brown for fall), so the legend is easy to remember. The segments are stacked in calendar order so the seasons line up across states. Washington leads by a wide margin with 553 reports, followed by California with 397 and Florida with 283. Every state peaks in summer or fall, and across all reports summer accounts for about 38% and fall for about 30%. That pattern fits with more people being outdoors hiking, camping, and hunting in those months.

For this plot I used all reports, including the ones with no coordinates, because location on a map isn't needed here. I dropped the 91 reports with an `Unknown` season, counted reports for each state and season combination with a pandas `groupby`, and kept only the 15 states with the most reports so the chart stays readable.

## Interactivity

Plot 1 has two linked interactions. First, you can click and drag across the timeline to select a range of years, and the map filters to show only reports from those years. Second, you can click a class in the legend to highlight only that class on the map; the timeline then updates to count only that class (shift-click to select more than one class). Together these let you ask questions that a single static map can't answer. Brushing 2002–2006 shows that the reporting boom around 2004 (241 reports, the peak year) happened across the whole country, with reports from 46 states, not in one hotspot. Isolating Class A shows that clear sightings aren't only a Pacific Northwest story: Washington has the most Class A reports, but Ohio, Florida, and Texas each have more than 100. The map alone shows only where reports happened; the brush adds when, and the legend filter adds how credible each report is.
