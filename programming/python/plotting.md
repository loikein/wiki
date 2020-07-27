# Plotting

## General

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
sns.someplot(…).set_title("This is a title")
```

### Axis

Set the x-axis and y-axis to same scale:

```python
plt.axis('equal')
fig, ax = plt.subplots()

ax.plot(…)
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

## Plot With `jointplot`

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

### Axis

```python
g.set_axis_labels(r"$x_1$", "y")
```

### Ticks

Set formatter:

```python
import matplotlib as mpl

g.ax_joint.get_yaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.0f}'))
g.ax_joint.get_xaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.4f}'))
```

