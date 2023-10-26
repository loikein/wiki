---
weight: 700
title: "Matplotlib/Seaborn"
---

> `seaborn` depends on `matplotlib`.
{.book-hint .info}

## \(Maybe\) Useful resources

- [Examples — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/gallery/index)
- [Example gallery — seaborn 0.12.2 documentation](https://seaborn.pydata.org/examples/index.html)
- [Python Graph Gallery](https://python-graph-gallery.com/)
- [Interactive Applications Using Matplotlib | Packt](https://www.packtpub.com/product/interactive-applications-using-matplotlib/9781783988846)
    + [examples / Interactive Applications Using Matplotlib · GitLab](https://resources.oreilly.com/examples/9781783988846)
- ["Artist" in Matplotlib - something I wanted to know before spending tremendous hours on googling how-tos. - DEV Community](https://dev.to/skotaro/artist-in-matplotlib---something-i-wanted-to-know-before-spending-tremendous-hours-on-googling-how-tos--31oo)


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

# Save as pdf
# Pro: keep words selectable;
# Con: could result in huge file
fig.savefig("fig-1.pdf")

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
ax.set_xlim(left=0, right=5)

# y-axis
ax.set_ylim(bottom=0, top=5)
```

Set axis to only use integer ticks: \([credit](https://stackoverflow.com/questions/12050393/how-to-force-the-y-axis-to-only-use-integers#comment110460128_38096332)\)

```python
ax.yaxis.get_major_locator().set_params(integer=True)
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
# if want to break lines, put outside r:
ax.set_xlabel("Something\n" + r"$x_1$")
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

### Annotation

Docs:

- [matplotlib.pyplot.annotate — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.annotate.html)
- [matplotlib.text — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/api/text_api.html)
- [Annotations — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/tutorials/text/annotations.html)

Usage: \([credit](https://stackoverflow.com/a/58669227/10668706)\)

```python
fig, ax = plt.subplots()
sns.boxplot(ax=ax, data=df, order=["Good", "Ok", "Bad"])

ax.annotate(
    r"$N=" + str(len(df[df["Rate"]=="Good"])) + "$",
    xy=(0,0.75),    # The actual coordinates of the axes
    ha='center',    # Short for horizontalalignment of **kwargs for text
    va='bottom',    # Short for verticalalignment of **kwargs for text
    fontsize=12,
)

ax.annotate(
    r"$N=" + str(len(df[df["Rate"]=="Ok"])) + "$",
    xy=(1,0.75), ha='center', va='bottom', fontsize=12,
)

ax.annotate(
    r"$N=" + str(len(df[df["Rate"]=="Bad"])) + "$",
    xy=(2,0.75), ha='center', va='bottom', fontsize=12,
)
```


## Plot With Subplots

Generally the above-mentioned methods will work with adding indices like: `ax[0,1].set_xlabel(r"$x_1$")`, etc.

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

### Plot size

If there are three subplots:

```python
fig, ax = plt.subplots(1, 3, figsize=(12, 4))
```

### Axis settings

Docs:

- [matplotlib.axes.Axes.tick_params — Matplotlib 3.8.0 documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.tick_params.html)
- [Linestyles — Matplotlib 3.8.0 documentation](https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html)

Ref: [How to Remove Ticks from Matplotlib Plots? - GeeksforGeeks](https://www.geeksforgeeks.org/how-to-remove-ticks-from-matplotlib-plots/)

Full example: create stick-together subplots with dashed line divider (to achieve something like [this](https://copyprogramming.com/howto/creating-a-boxplot-facetgrid-in-seaborn-for-python#box-plot-with-divisor-in-seaborn-python), but with wide data and not using seaborn)

```python
fig1, axes1 = plt.subplots(
    1, 4,
    figsize=(7, 5),
    sharex=True,
    sharey=True,
    # remove gap, vertical: "hspace": 0
    gridspec_kw={"wspace": 0},
)

# Plot here
# axes1[0].plot(...)

for ax in axes1:
    # Set ylim
    ax.set_ylim([0, 0.02])
    
    # Set xticks and yticks to face inside of graph
    ax.tick_params(direction="in", labelbottom=False)

    # Get rid of all ticks
    # ax.tick_params(left=False, bottom = False, labelleft=False, labelbottom=False)

    # Get rid of all xtick labels (method 1)
    # ax.tick_params(labelbottom=False)

    # Get rid of all xtick labels (method 2)
    # ax.axes.get_xaxis().set_ticklabels([])

    # Keep only a list of xticks and labels:
    ax.set_xticks(["2020-05", "2020-08"])

# Remove ticks and make dashed axes (spines)
# Credit: https://stackoverflow.com/a/55949863
for i in range(1, 3+1):
    axes1[i].tick_params(left=False)
    axes1[i].spines["left"].set_linestyle((0,(8,5)))

fig1.tight_layout()
fig1.savefig(os.path.join("fig", "huge-fig.pdf"))
```

### Plot into subplots

```python
fig1, axes1 = plt.subplots(1, 4, figsize=(7, 5))
fig1.suptitle("Big title")

# Line plots:
axes1[0].plot(df1, linewidth=1)
axes1[0].set_xlabel("Df 1")
# Or title, but titles cannot be placed under subplots
# axes1[0].set_title("Df 1")

# Scatter plots:
axes1[1].plot(df2, 'o', alpha=0.01, color="#4c72b0")
axes1[1].set_xlabel("Df 2")

# Linked scatter plots:
axes1[2].plot(df3, 'o-', alpha=0.01, color="#4c72b0")
axes1[2].set_xlabel("Df 3")

axes1[3].plot(df4, linewidth=1)
axes1[3].set_xlabel("Df 4")
```

### Plot into subplots with Seaborn

Doc: [Overview of seaborn plotting functions — seaborn 0.12.2 documentation](https://seaborn.pydata.org/tutorial/function_overview.html#figure-level-vs-axes-level-functions)

> Also works for single plots:
> 
> ```python
> fig, ax = plt.subplots()
> # draws on top of previous layers
> sns.histplot(ax=ax, ...)
> 
> # overwrites previous layers
> ax = sns.histplot(...)
> ```
{.book-hint .info}

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
fig1.savefig(os.path.join("plot", "fig1.pdf"))
fig1.show() # or if in Jupyter: fig1
```


## Seaborn

### Use `**kwargs`

Doc: [Frequently asked questions — seaborn 0.12.2 documentation](https://seaborn.pydata.org/faq.html?highlight=kwargs#other-customizations)

For a list of all options see the `**kwargs` portion of: [matplotlib.axes.Axes.plot — Matplotlib 3.7.2 documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.plot.html)


### Plot With `jointplot`

<!-- [python - Seaborn jointplot -- change bandwidth of both marginal plots - Stack Overflow](https://stackoverflow.com/questions/52389106/seaborn-jointplot-change-bandwidth-of-both-marginal-plots) -->

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

### Heatmap

Ref: [Plotting a diagonal correlation matrix — seaborn 0.12.2 documentation](https://seaborn.pydata.org/examples/many_pairwise_correlations.html)

```python
corr = df.corr()
mask = np.triu(np.ones_like(corr, dtype=bool))
# These two are identical:
cmap = sns.color_palette("light:#4c72b0", as_cmap=True)
cmap = sns.color_palette("blend:#FFF,#4c72b0", as_cmap=True)
# If want to check:
cmap

fig1, ax1 = plt.subplots(figsize=(11, 9))
sns.heatmap(
    corr,
    ax=ax1,
    mask=mask,
    cmap=cmap,
    vmax=1, vmin=0,     # do not set in the first pass!!
    square=True,
    linewidths=.5,
    cbar_kws={"shrink": .5},
)
```

### Pair plot

Docs:

- [seaborn.pairplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.pairplot.html)
- Diagonal:
  + [seaborn.histplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.histplot.html)
  + [seaborn.kdeplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.kdeplot.html)
- Off-diagonal:
  + [seaborn.scatterplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.scatterplot.html#seaborn.scatterplot)
  + [seaborn.regplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.regplot.html?highlight=regplot)
  + [seaborn.kdeplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.kdeplot.html)

No regression:

```python
fig, ax = plt.subplots()

sns.pairplot(
    ax=ax,
    data=df,
    kind="kde",                             # if want kdeplot everywhere
    diag_kind="kde",                        # if want kdeplot diagonals
    diag_kws=dict(linewidth=0),             # for the histplot
    plot_kws=dict(linewidth=0, alpha=0.3),  # for the scatterplot
)
```

Use regression: \([credit](https://stackoverflow.com/a/50724511)\)

```python {hl_lines="6 8-11"}
fig, ax = plt.subplots()

sns.pairplot(
    ax=ax,
    data=df,
    kind="reg",
    diag_kws=dict(linewidth=0),
    plot_kws=dict(
        line_kws=dict(linewidth=2, color="black"),  # for the regplot
        scatter_kws=dict(linewidth=0, alpha=0.3),   # for the scatterplot
    ),
)
```

### Scatter plot

Doc: [seaborn.scatterplot — seaborn 0.12.2 documentation](https://seaborn.pydata.org/generated/seaborn.scatterplot.html)

```python
fig, ax = plt.subplots()

sns.scatterplot(
    ax=ax,
    data=df,
    x="X",
    y="Y",
    hue="Type",     # For marker colours
    style="Type",   # For marker shapes
    linewidth=0,
    alpha=0.3,
)
```

### Violin plot

Ref: [alpha does not work with violinplot · Issue #622 · mwaskom/seaborn](https://github.com/mwaskom/seaborn/issues/622#issuecomment-329378520)

```python
fig4, ax4 = plt.subplots()

sns.violinplot(
    ax=ax4,
    data=data_df, x="Categories", y="Numbers",
    inner=None,          # Hide miniature boxplots inside
    order=order=["Good", "Ok", "Bad"],
    linewidth=0,         # Cannot be used with inners other than None
    palette="viridis",
    # color="#069AF3",   # All the same colour
    bw=0.05,             # Reduce smoothing
    # These do not work for some reason:
    # showmeans=False,
    # showmedians=True,
)

plt.setp(ax4.collections, alpha=.5)
```

### Boxplot; Controlling zorder of plot layers

Slightly modified from: [python - How to display boxplot in front of violinplot in seaborn - seaborn zorder? - Stack Overflow](https://stackoverflow.com/a/68614885)

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.rand(10, 2)).melt(var_name='group')

ax = sns.violinplot(
    data=df, x='group', y='value',
    color="#af52f4",
    inner=None,
    linewidth=0,
)

sns.boxplot(
    ax=ax,
    data=df, x='group', y='value',
    saturation=0.5,                 # Colour of box face (filling)
    width=0.4,                      # Scale Width of box
    palette='rocket',
    # flierprops={"marker": "o"},   # Set outliers' markers
    showfliers = False,             # Hide outliers
    linewidth=2,
    boxprops={"facecolor": "none", "zorder": 2},  # Make the boxes completely transparent
)

plt.show()
```


## Problem with plots

[Data to Viz | A collection of graphic pitfalls](https://www.data-to-viz.com/caveats.html)

### Boxplot

Problem with boxplots: [Hidden Data Under Boxplot](https://python-graph-gallery.com/39-hidden-data-under-boxplot/), [The Boxplot and its pitfalls](https://www.data-to-viz.com/caveat/boxplot.html)

- Show jitter dots
- Show number of observations
- Use Violin plot instead
