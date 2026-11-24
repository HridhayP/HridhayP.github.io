---
name: "Richer Countries, Bigger Footprints"
tools: [Python, Altair, vega-lite]
image: /assets/pngs/co2_dashboard.png
description: IS 445 Final Project - how a country's wealth relates to how much CO2 it emits
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---

# Richer Countries, Bigger Footprints: How Wealth Shapes CO2 Emissions

**By Hridhay Prabahar** (group of 1: Hridhay Prabahar)

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/owid/co2-data/master/owid-co2-data.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/HridhayP/HridhayP.github.io/blob/main/python_notebooks/fp3_co2.ipynb" text="The Analysis" %}
</div>

Carbon dioxide (CO2) is the main gas behind climate change, and it mostly comes from burning coal, oil, and gas for electricity, cars, and factories. Every country emits some, but the amounts are very different. A person in the United States is responsible for about 15 tonnes of CO2 a year, while a person in India is responsible for about 2. This page looks at one big reason for that gap: how rich a country is.

## How the world got here

<vegachart schema-url="{{ site.baseurl }}/assets/json/co2_world_sources.json" style="width: 100%"></vegachart>

The world emitted about 2 billion tonnes of CO2 in 1900. Today it is close to 39 billion tonnes, almost 20 times more. The chart stacks each source on top of the others so the total height is the world's emissions in that year. Coal was nearly the only source in 1900 and is still the biggest one today, while oil and gas grew quickly after 1950 as cars, planes, and power plants spread around the world. Each source gets its own color because the sources are separate categories, not a scale from low to high. The small dips line up with events that slowed the economy, like the 2008 financial crisis and the 2020 COVID lockdowns, which is a first hint that emissions follow economic activity.

## Wealth and emissions, country by country

<vegachart schema-url="{{ site.baseurl }}/assets/json/co2_dashboard.json" style="width: 100%"></vegachart>

**How to use this chart:** Each circle in the top-left chart is a country. Moving right means the average person there earns more (GDP per person), and moving up means the average person there emits more CO2. Bigger circles are countries with more people. Use the **Year** slider under the charts to go back in time to 1990. Click and drag a box over any group of circles, and the bar chart on the right will show the 15 biggest total emitters in that group. Click a bar to add that country's line to the bottom chart (hold shift to pick more than one), and double-click the scatter plot to reset. Hover over anything to see the exact numbers.

The circles form a clear line going up and to the right: richer countries emit much more CO2 per person. Both axes use a log scale, which means each step is 10 times bigger than the last one. I used it because incomes range from a few hundred dollars to over $100,000 per person, and on a normal scale almost every country would be squished into one corner. The bottom chart shows that the relationship isn't fixed, though. The United States has gotten a lot richer since 2000, but its emissions per person dropped from about 21 tonnes to about 15, mostly because power plants switched from coal to gas and renewables. Meanwhile China's emissions per person almost quadrupled as its economy grew, and India's are rising slowly from a low starting point.

## Who emitted the most over time

<vegachart schema-url="{{ site.baseurl }}/assets/json/co2_cumulative.json" style="width: 100%"></vegachart>

CO2 stays in the air for centuries, so what matters for warming is the total amount a country has emitted over its history, not only what it emits today. This bar chart adds up every year since 1750. China emits the most per year right now, but the United States has emitted the most overall (about 23% of all CO2 ever released by countries), and countries that got rich early, like the United Kingdom and Germany, rank much higher here than they do on yearly emissions. This is why wealth matters for the climate debate in two ways: rich countries are both the biggest emitters per person today and the ones that caused most of the warming so far, while poorer countries are trying to grow their economies now, which has usually meant emitting more.

## Sources

- **Main dataset:** Hannah Ritchie, Pablo Rosado, and Max Roser (2023). "CO2 and Greenhouse Gas Emissions." Published online at OurWorldinData.org. Data: [github.com/owid/co2-data](https://github.com/owid/co2-data) (CC BY 4.0). The CO2 numbers come from the Global Carbon Project's [Global Carbon Budget](https://globalcarbonbudget.org), GDP from the Maddison Project Database, and population from UN World Population Prospects.
- **Contextual visualizations:** Both contextual charts ("World CO2 emissions by source" and "Top 15 countries by total CO2 emitted") were made by me from the same Our World in Data dataset. The code for them, and for the main chart, is in [my analysis notebook](https://github.com/HridhayP/HridhayP.github.io/blob/main/python_notebooks/fp3_co2.ipynb).
