---
weight: 200
title: "Documentation"
---

# Documentation

## References

Documentation:

* [numpydoc docstring guide — numpydoc v1.1.dev0 Manual](https://numpydoc.readthedocs.io/en/latest/format.html)
* [Example — numpydoc v1.1.dev0 Manual](https://numpydoc.readthedocs.io/en/latest/example.html#example)
* [sampledoc tutorial — sampledoc 1.0 documentation](https://matplotlib.org/sampledoc/)

General reST:

* [A ReStructuredText Primer](https://docutils.sourceforge.io/docs/user/rst/quickstart.html)
* [reStructuredText Markup Specification](https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#syntax-details)
* More details: [reStructuredText Directives](https://docutils.sourceforge.io/docs/ref/rst/directives.html)

## Sphinx basics

Under `./docs/`:

```bash
$ conda activate my_env

# the following two are same if makefile exists
$ sphinx-build  -M html source build
$ make html

# open in default browser
$ open build/html/index.html
```

### Example Folder Tree

```text
.
├── docs
│   ├── Makefile
│   ├── _static
│   │   └── images
│   │       └── image.jpg
│   └── source
│       └── document_file.rst
└── code
    ├── __init__.py
    └── main_code.py
```

### Example `makefile`

```make
# Minimal makefile for Sphinx documentation

# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= sphinx-build
SOURCEDIR     = .
BUILDDIR      = _build
LATEXMKOPTS   = "-xelatex"

# Put it first so that "make" without argument is like "make help".
help:
    @$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
    @$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
```


## Working Example from [OpenSourceEconomics/temfpy](https://github.com/OpenSourceEconomics/temfpy)

```python
def eoq_model(x, r=0.1):
    r"""Economic order quantity model.

    This function computes the optimal economic order quantity (EOQ) based on the model presented in
    [H1990]_. The EOQ minimizes the holding costs as well as ordering costs. The core parameters of
    the model are the units per months `x[0]`, the unit price of items in stock `x[1]`,
    and the setup costs of an order `x[2]`. The annual interest rate `r` is treated as an
    additional parameter.

    .. math::
        y = \sqrt{\frac{24 x_0 x_2}{r x_1}}

    .. image:: ../../docs/_static/images/image.jpg
       :align: center
       :alt: place holder image

    Parameters
    ----------
    x : array_like
        Core parameters of the model

    r : float, optional
        Annual interest rate (default value is 0.1)

    Returns
    -------

    y : float
        Optimal order quantity

    Notes
    -----

    A historical perspective on the model is provided by [E1990]_. A brief description with the core
    equations is available in [W2020]_.

    References
    ----------

    .. [H1990] Harris, F. W. (1990).
        How many parts to make at once.
        Operations Research, 38(6), 947–950.

    .. [E1990] Erlenkotter, D. (1990).
        Ford Whitman Harris and the economic order quantity model.
        Operations Research, 38(6), 937–946.

    .. [W2020] Economic order quantity. (2020, April 3). In Wikipedia.
        Retrieved from
        `https://en.wikipedia.org/w/index.php\
        ?title=Economic_order_quantity&oldid=948881557 <https://en.wikipedia.org/w/index.php
        ?title=Economic_order_quantity&oldid=948881557>`_

    Examples
    --------

    >>> x = [1, 2, 3]
    >>> y = eoq_model(x, r=0.1)
    >>> np.testing.assert_almost_equal(y, 18.973665961010276)
    """
    # No blank line is allowed for functions.
    m, c, s = x
    y = np.sqrt((24 * m * s) / (r * c))

    return y
```

## reStructuredText basics

### Variables

[I have reported a bug](https://github.com/sphinx-doc/sphinx/issues/7780) that stops combined parameters from rendering.

```text
Parameters
----------
x : type
    Description of `x`. Type can be ``int``, ``float``, etc.
    Note that this breaks when there are multiple variables.

a : type, optional
    Description of `a` (default values is 10).
    Note that this breaks when there are multiple variables.

type c, d, e
    Description of `c`, `d` and `e`.
    The only way to get multiple variables in the same line.
```

### Image

If in `document_file.rst`:

```text
.. image:: ../../_static/images/image.jpg
   :align: center
   :alt: a great image
```

If in `main_code.py`:

```text
.. image:: ../../docs/_static/images/image.jpg
   :align: center
   :alt: a great image
```

### Hyperlinks

Note: the text must have same indentation as the URL it's referring to, see example:

```text
Some text

    Some indented text `a link that points outwards with long URL`_.

    .. _a link that points outwards with long URL: https://chaospy.readthedocs.io/
    en/master/search.html?q=sobol&check_keywords=yes&area=default
```

### Math

Both inline and block math will work.

```text
.. math:: y = \sqrt{\frac{24 x_0 x_2}{r x_1}}

:math:`y = \sqrt{\frac{24 x_0 x_2}{r x_1}}`
```

## Debugging

More like de-warning.

### Inline interpreted text or phrase reference start-string without end-string.

Ref: [Documentation Guide for Devs](https://developer.mantidproject.org/Standards/DocumentationGuideForDevs.html#inline-interpreted-text-or-phrase-reference-start-string-without-end-string)

All non-inline math in `.ipynb` files should be surrounded by either of the following: (probably non-exhaustive but I'm too tired to try others)

- `\begin{aligned} … \end{aligned}`
- `$$ … $$`

While the followings are forbidden even if then render just fine in Jupyter Notebook. Sphinx just won't have it.

- `\begin{align} … \end{align}`
- `\begin{equation} … \end{equation}`

### Document or section may not begin with a transition.

Ref: 

- [Docutils: Documentation Utilities / Re: [Docutils-develop] Section may not end with a transition?](https://sourceforge.net/p/docutils/mailman/message/6975902/)
- [reStructuredText Markup Specification](https://docutils.sourceforge.io/docs/ref/rst/restructuredtext.html#transitions)

Do this:

```markdown
## Blah

Blah blah blah
```

Don't do this:

```markdown
## Blah
---

Blah blah blah
```

The same for reStructuredText.
