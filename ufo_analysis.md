---
layout: post
title: UFO Sightings Analysis
---

# UFO Sightings Analysis  
**by Rahul Balasubramani**  
**Date: November 12, 2025**

---

<script src="https://cdn.jsdelivr.net/npm/vega@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>

# UFO Sightings in the USA (1950-2014)

## Visualization 1: Geographic Distribution of UFO Sightings

<div id="vis1"></div>
<script type="text/javascript">
  var spec = "/assets/json/df_ufo_map.json";
  vegaEmbed('#vis1', spec).then(function(result) {
  }).catch(console.error);
</script>

### Description
This plot shows where UFO sightings happened across the U.S. from 1950 to 2014. Each point is one sighting and I used a sample of 5,000 dataset so the map loads smoothly instead of freezing. The idea here was mainly to see how these reports are spread out and whether certain areas seem to have more sightings than others.

### Design Choices

I used a basic map with longitude on the x-axis and latitude on the y-axis. I picked the Albers USA projection since it makes the U.S. look properly on screen. Each point is colored based on the shape that was reported (like “light,” “circle,” “triangle,” etc.). I used the Category20 color scheme because there are a lot of shapes and this palette gives me enough distinct colors without everything blending together. The points are a little transparent so overlapping sightings don’t completely cover each other up.

### Data Transformations

Before plotting, I cleaned the dataset by:
- Keeping only the U.S. sightings
- Dropping rows with missing latitude, longitude, shape, or year
- Making sure the coordinates fall within rough U.S. boundaries
- Using only years from 1950–2014
- Randomly selecting 5,000 sightings from the full dataset to reduce overplotting

This made the dataset a lot more manageable and kept the map readable and fast.

---

## Visualization 2: UFO Sightings Over Time by Shape

<div id="vis2"></div>
<script type="text/javascript">
  var spec = "/assets/json/df_ufo_timeseries.json";
  vegaEmbed('#vis2', spec).then(function(result) {
  }).catch(console.error);
</script>

### Description

This visualization looks at how UFO sightings changed over time and compares different shapes people reported. It covers the same years as the map (1950–2014) and shows how often each of the top 10 shapes appeared in each year. It’s basically a way to see whether certain shapes became more common or faded out.

### Design Choices

I used a line chart because trends over time are easiest to understand this way. Year goes on the x-axis and the number of sightings goes on the y-axis. Each shape gets its own line and I added little points to make each year stand out. I used the Tableau20 color scheme so each shape has its own color that’s easy to tell apart. I limited the plot to the top 10 shapes to keep it from getting too messy.

### Data Transformations

Additional transformations for this visualization:
- Parsed the datetime column and pulled out the year
- Re-used the cleaned U.S. data from the first plot
- Found the top 10 shapes overall
- Grouped the dataset by year and shape to count how many sightings happened each year

This turned the full dataset into a nice small table that works well for a time-series plot.

---

## Interactivity: Shape Selection Dropdown

The second plot includes a dropdown menu that lets you choose which UFO shape you want to focus on. When you pick a shape, that line stays bright while the others fade into the background. This makes it much easier to compare shapes without having to stare at a tangle of lines. You can still switch back to “all shapes” to see the big picture again.

This interaction is helpful because:

- It keeps the main plot from feeling overwhelming
- You can compare shapes one-by-one
- It highlights patterns you’d probably miss otherwise (like certain shapes suddenly becoming popular in certain decades)

Overall, the dropdown makes the chart much easier to explore, instead of having everything displayed at full opacity all the time.

---

## Links

**[The Data](https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/ufo-scrubbed-geocoded-time-standardized-00.csv)**

**[The Analysis](https://github.com/rahulb0206/rahulb0206.github.io/blob/main/Workbook.ipynb)**