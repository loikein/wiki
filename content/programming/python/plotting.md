---
weight: 700
title: "Plotting"
---

{{< hint info >}}
`seaborn` depends on `matplotlib`.
{{< /hint >}}

Refs:

- [Examples — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/gallery/index)
- [Example gallery — seaborn 0.12.2 documentation](https://seaborn.pydata.org/examples/index.html)
- [Python Graph Gallery](https://python-graph-gallery.com/)


## General

Doc: [Matplotlib Application Interfaces (APIs) — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/users/explain/api_interfaces.html)

Start plotting:

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.clf()
fig, ax = plt.subplots()

# If want subplots:
fig, ax = plt.subplots(1,3)
```

End plotting: \([credit](https://stackoverflow.com/questions/6541123/improve-subplot-size-spacing-with-many-subplots-in-matplotlib)\)

```python
# Show legend:
ax.legend()

# If there are multiple subplots:
fig.tight_layout()

# Save as png
fig.savefig("fig-1")

# Show on screen
fig.show()
```

### Add Straight Lines

Vertical line at given position:

```python
# Add dashed vertical line at x=2190:
ax.axvline(2190, linestyle="--", color="lightgrey")
```

Horizontal line at given position:

```python
# Add dotted horizontal line at y=20:
ax.axhline(20, linestyle=":", color="lightgrey")
```

Line connecting any two points:

```python
# Draw a line between (x1,y1) and (x2,y2):
ax.plot([x1, x2], [y1, y2])
```

### Colours

Any `colormap` can be reversed by adding `_r` after its name, e.g. `cmap="RdBu_r"` makes the smaller value blue and the bigger value red.

### Title

Seaborn:

```python
sns.someplot(...).set_title("This is a title")
```

### Axis

Set the x-axis and y-axis to same scale:

```python
plt.axis('equal')
fig, ax = plt.subplots()

ax.plot(...)
```

Set limit of each axis:

```python
fig, ax = plt.subplots()

# x-axis
ax.set_xlim(left=0)

# y-axis
ax.set_ylim(bottom=0)
```

### Ticks

Adjust label formats:

\(In this examle, the numbers will have thousand separators and/or 4 digit decimals.\)

```python
import matplotlib as mpl

fig, ax = plt.subplots()

ax.xaxis.set_major_formatter(mpl.ticker.StrMethodFormatter("{x:,.4f}"))
ax.yaxis.set_major_formatter(mpl.ticker.StrMethodFormatter("{x:,.0f}"))
```

Manually specify tick position & corresponding labels:

```python
fig, ax = plt.subplots()

pos = [1000, 2000, 2190, 3000, 4000]
lab = ["1,000", "2,000", r"$X^*$", "3,000", "4,000"]
ax.set_xticks(pos)
ax.set_xticklabels(lab)
```

Set label that includes LaTeX maths:

```python
fig, ax = plt.subplots()

ax.set_xlabel(r"$x_1$")
```

Erase all labels:

```python
ax.axes.get_yaxis().set_ticklabels([])
```

Adjust position of labels:

```python
# Make the second label of x-axis a little bit left:
ax.xaxis.get_majorticklabels()[1].set_horizontalalignment("right")
```

## Plot With Subplots

Generally the above-mentioned methods will work with adding indices like: `ax[0,1].set_xlabel(r"$x_1$")`, etc.


### Plot into subplots with Seaborn

Doc: [Overview of seaborn plotting functions — seaborn 0.12.2 documentation](https://seaborn.pydata.org/tutorial/function_overview.html#figure-level-vs-axes-level-functions)

{{< hint info >}}
Also works for single plots:

```python
fig, ax = plt.subplots()
sns.histplot(ax=ax, ...)

# or
ax = sns.histplot(...)
```
{{< /hint >}}

Ref: [ds-micro-tutorials/data-analysis/subplotting.ipynb](https://github.com/thalesbruno/ds-micro-tutorials/blob/master/data-analysis/subplotting.ipynb)

```python
fig1, axes1 = plt.subplots(2, 2, figsize=(10, 10))
fig1.suptitle("Big title")

sns.histplot(ax=axes1[0,0], data=df1, x="Rating", binwidth=0.1)
axes1[0,0].set_title("Subtitle 1-1")

sns.histplot(ax=axes1[0,1], data=df2, x="Rating", binwidth=0.1)
axes1[0,1].set_title("Subtitle 1-2")

sns.histplot(ax=axes1[1,0], data=df3, x="Rating", binwidth=0.1)
axes1[1,0].set_title("Subtitle 2-1")

sns.histplot(ax=axes1[1,1], data=df4, x="Rating", binwidth=0.1)
axes1[1,1].set_title("Subtitle 2-2")

fig1.tight_layout()
fig1.savefig(os.path.join("plot", "fig1"))
fig1.show() # or if in Jupyter: fig1
```

### Title

Main title: \([credit](https://stackoverflow.com/a/29814281/10668706)\)

```python
fig, ax = plt.subplots(2,2)

plt.subplots_adjust(top=0.9)
grid.fig.suptitle("This is a big title")
```

Sub titles: `ax[0, 0].set_title('Axis [0, 0]')`

```python
fig, ax = plt.subplots(2,2)

ax[1, 0].set_title(r"$X_2$ vs $Y_1$")
```

### Total size

If there are three subplots:

```python
fig, ax = plt.subplots(1, 3, figsize=(12, 4))
```

## Seaborn

### Use `**kwargs`

Doc: [Frequently asked questions — seaborn 0.12.2 documentation](https://seaborn.pydata.org/faq.html?highlight=kwargs#other-customizations)

For a list of all options see the `**kwargs` portion of: [matplotlib.axes.Axes.plot — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.plot.html)


### Plot With `jointplot`

Make the figure:

```python
import matplotlib.pyplot as plt
import seaborn as sns

g = sns.jointplot(x=x[1], y=y, kind="hex")
```

Show the figure:

```python
g.fig
```

#### Axis

```python
g.set_axis_labels(r"$x_1$", "y")
```

#### Ticks

Set formatter:

```python
import matplotlib as mpl

g.ax_joint.get_yaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.0f}'))
g.ax_joint.get_xaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.4f}'))
```

### Order categorical axis

[Visualizing categorical data — seaborn 0.12.2 documentation](https://seaborn.pydata.org/tutorial/categorical.html)

Add param in plot function: `order=["Good", "Ok", "Bad"]` \(also works with string variables\)


## Problem with plots

[Data to Viz | A collection of graphic pitfalls](https://www.data-to-viz.com/caveats.html)

### Boxplot

Problem with boxplots: [Hidden Data Under Boxplot](https://python-graph-gallery.com/39-hidden-data-under-boxplot/), [The Boxplot and its pitfalls](https://www.data-to-viz.com/caveat/boxplot.html)

- Show jitter dots
- Show number of observations
- Use Violin plot instead
