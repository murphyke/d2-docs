---
sidebar_label: Text & Code
pagination_next: tour/icons
---
# Text

## Standalone text is Markdown

```d2
explanation: |md
  # I can do headers
  - lists
  - lists

  And other normal markdown stuff
|
```

<div style={{width: 300, margin: "0 auto"}} className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/markdown.svg2')}}></div>

## Most languages are supported

D2 most likely supports any language you want to use, including non-Latin ones like
Chinese, Japanese, Korean, even emojis!

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/unicode.svg2')}}></div>

## LaTeX

You can use `latex` or `tex` to specify a LaTeX language block.

```d2
plankton -> formula: will steal
formula: {
  equation: |latex
    \\lim_{h \\rightarrow 0 } \\frac{f(x+h)-f(x)}{h}
  |
}
```

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/text-2.svg2')}}></div>

A few things to note about LaTeX blocks:

- You must escape `\`, as these are escape characters. Note the usage of `\\` in the above
  example.
- LaTeX blocks do not respect `font-size` styling. Instead, you must style these inside
  the Latex script itself with commands:
  - `\tiny{ }`
  - `\small{ }`
  - `\normal{ }`
  - `\large{ }`
  - `\huge{ }`
- Under the hood, this is using [MathJax](https://www.mathjax.org/). It is not full LaTeX
  (full LaTeX includes a document layout engine). D2's LaTeX blocks are meant to display
  mathematical notation, but not support the format of existing LaTeX documents. See
  [here](https://docs.mathjax.org/en/latest/input/tex/macros/index.html) for a list of all
  supported commands.

:::caution
D2 runs on the latest version of MathJax, which has a lot of nice things but unfortunately
does not have linebreaks. You can kind of get around this with the `displaylines` command.
See below.
:::

:::note
Currently cannot be applied to labels, which is why the above example nests an object.
This is coming soon.
:::

## Code

Change `md` to a programming language for code blocks

```d2
explanation: |go
  awsSession := From(c.Request.Context())
  client := s3.New(awsSession)

  ctx, cancelFn := context.WithTimeout(c.Request.Context(), AWS_TIMEOUT)
  defer cancelFn()
|
```

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/code-2.svg2')}}></div>

## Advanced: Non-Markdown text

In some cases, you may want non-Markdown text. Maybe you just don't like Markdown, or the
GitHub-styling of Markdown that D2 uses, or you want to quickly change a shape to text.
Just set `shape: text`.

```d2
title: A winning strategy {
  shape: text
  near: top-center
  style: {
    font-size: 55
    italic: true
  }
}

poll the people -> results
results -> unfavorable -> poll the people
results -> favorable -> will of the people
```

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/non-markdown-text.svg2')}}></div>

## Advanced: Block strings

What if you're writing Typescript where the pipe symbol `|` is commonly used? Just add
another pipe, `||`.

```d2
my_code: ||ts
  declare function getSmallPet(): Fish | Bird;
||
```

Actually, Typescript uses `||` too, so that won't work. Let's keep going.

```d2
my_code: |||ts
  declare function getSmallPet(): Fish | Bird;
  const works = (a > 1) || (b < 2)
|||
```

There's probably some language or scenario where the triple pipe is used too. D2 actually
allows you to use any special symbols (not alphanumeric, space, or `_`) after the first pipe:

```d2
# Much cleaner!
my_code: |`ts
  declare function getSmallPet(): Fish | Bird;
  const works = (a > 1) || (b < 2)
`|
```

## Advanced: LaTeX plugins

D2 includes the following LaTeX plugins:

```d2
amscd plugin: {
  ex: |tex
    \\begin{CD} B @>{\\text{very long label}}>> C S^{{\\mathcal{W}}_\\Lambda}\\otimes T @>j>> T\\\\ @VVV V \\end{CD}
  |
}

braket plugin: {
  ex: |tex
    \\bra{a}\\ket{b}
  |
}

cancel plugin: {
  ex: |tex
    \\cancel{Culture + 5}
  |
}

color plugin: {
  ex: |tex
    \\textcolor{red}{y} = \\textcolor{green}{\\sin} x
  |
}

gensymb plugin: {
  ex: |tex
    \\lambda = 10.6\\,\\micro\\mathrm{m}
  |
}

mhchem plugin: {
  ex: |tex
    \\ce{SO4^2- + Ba^2+ -> BaSO4 v}
  |
}

physics plugin: {
  ex: |tex
    \\var{F[g(x)]}
    \\dd(\\cos\\theta)
  |
}

multilines: {
  ex: |tex
    \\displaylines{x = a + b \\\\ y = b + c}
    \\sum_{k=1}^{n} h_{k} \\int_{0}^{1} \\bigl(\\partial_{k} f(x_{k-1}+t h_{k} e_{k}) -\\partial_{k} f(a)\\bigr) \\,dt
  |
}

# Just to separate into two rows
amscd plugin -> braket plugin: {style.opacity: 0}
cancel plugin -> color plugin: {style.opacity: 0}
gensymb plugin -> mhchem plugin: {style.opacity: 0}
physics plugin -> multilines: {style.opacity: 0}
```

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/latex.svg2')}}></div>
