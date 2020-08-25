---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.2'
      jupytext_version: 1.4.2
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

## FJ's attempts at interactive zoom into a graph 

1. DONE IN FJtest01: First plot some data (not using dates - need to learn more about formats etc.)
2. DONE IN FJtest02: Then change the min/mx on axes with sliders, which equals adjusting "scales"
3. Then add selection interactivity
4. then use selection interactivity result to change axes. 
5. convert to use dataframes.

```python
import pandas as pd
import numpy as np
import bqplot.pyplot as plt
from bqplot import (LinearScale, Axis, Figure, OrdinalScale, DateScale, Bars, Lines, Scatter)
import ipywidgets as widgets
from ipywidgets import HBox, VBox, HTML

dfs = pd.read_csv("data/YVR-2017.csv",index_col=0, parse_dates=['DATE_PST'])
# dfs
# dfs[23:25]
```

```python
# Two vectors x and y (not using dates for x yet) 
y = dfs["RAW_VALUE"]
# x = dfs.index
x = np.arange(len(dfs))

# 1. Create the scales
# xs = DateScale()
xs = LinearScale()
ys = LinearScale()

# x[:5]
```

```python
# 2. Create the axes for x and y
xax = Axis(scale=xs, label='Date')
yax = Axis(scale=ys, orientation='vertical', label='O_3')

# 3. Create a Scatter mark by passing in the scales
# note that Scatter object is stored in `scatter` which can be used later to update the plot
scatter = Scatter(x=x, y=y, scales={'x': xs, 'y': ys}, colors=['red'], stroke='black', default_size=32)
```

```python
from bqplot.interacts import (
    FastIntervalSelector, IndexSelector, BrushIntervalSelector,
    BrushSelector, MultiSelector, LassoSelector, PanZoom, HandDraw
)

# br_sel.selected is a 2x2 array with [[xmin, ymin], [xmax, ymax]]
br_sel = BrushSelector(x_scale=xs, y_scale=ys, marks=[scatter], color='red')

db_scat_brush = HTML(value='[]')

## call back for the selector
def brush_callback(change):
    db_scat_brush.value = str(br_sel.selected)  
    
```

```python
br_sel.observe(brush_callback, names=['brushing'])

fig_scat_brush = Figure(marks=[scatter], axes=[xax, yax], title='Scatter Chart Brush Selector Example',
                        interaction=br_sel)

VBox([db_scat_brush, fig_scat_brush])
```

```python
xmin = br_sel.selected[0,0]
xmax = br_sel.selected[1,0]
ymin = br_sel.selected[0,1]
ymax = br_sel.selected[1,1]
    
# Create the axes for x and y
xs2 = LinearScale(min=xmin, max=xmax)
ys2 = LinearScale(min=ymin, max=ymax)
xax2 = Axis(scale=xs2, label='Date')
yax2 = Axis(scale=ys2, orientation='vertical', label='O_3')

line = Lines(x=x, y=y, scales={'x': xs2, 'y': ys2})
    
fig = Figure(marks=[line], axes=[xax2, yax2])    
fig
```

```python

```
