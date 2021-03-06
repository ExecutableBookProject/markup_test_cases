# Example syntax for myst

As a base, Myst adheres to the [CommonMark specification](https://spec.commonmark.org/).
For this, it uses the [Mistletoe project](https://github.com/miyuchina/mistletoe),
which is a well-structured markdown parser for Python that is CommonMark-compliant
and also extensible.

Myst adds several new syntax options that extend its functionality to be used
with Sphinx, the documentation generation engine used extensively in the Python
ecosystem. Sphinx uses reStructuredText by default, which is both more
powerful than Markdown, and also (arguably) more complex to use.

This project is an attempt to have the best of both worlds: the flexibility
and extensibility of Sphinx with the simplicity and readability of Markdown.

Here are a few major extensions from the CommonMark flavor of markdown

# Directives - a block-level extension point

Directives syntax is defined with triple-backticks and curly-brackets. It
is effectively a code block with curly brackets around the language, and
a directive name in place of a language name. It is similar to how RMarkdown
defines "runnable cells". Here is the basic structure

````
```{directivename} Directive arguments
---
optional: yaml
keyval: parameterization
---
My directive content.
```
````

For example, the following code:

````
```{admonition} This is my admonition
This is my note
```
````

Will generate this admonition:

```{admonition} This is my admonition
This is my note
```

For directives that are meant to parse content for your site, you may use
markdown as the markup language inside...

````
```{admonition} My markdown link
Here is [markdown link syntax](https://jupyter.org)
```
````

```{admonition} My markdown link
Here is [markdown link syntax](https://jupyter.org)
```

## Parameterizing directives

For directives that take parameters as input, you may parameterize them by
beginning your directive content with YAML frontmatter. This needs to be
surrounded by `---` lines. Everything in between will be parsed by YAML and
passed as keyword arguments to your directive. For example:

````
```{code-block} python
---
lineno-start: 10
emphasize-lines: 1, 3
caption: |
    This is my
    multi-line caption. It is *pretty nifty* ;-)
---
a = 2
print('my 1st line')
print(f'my {a}nd line')
```
````

```{code-block} python
---
lineno-start: 10
emphasize-lines: 1, 3
caption: |
    This is my
    multi-line caption. It is *pretty nifty* ;-)
---
a = 2
print('my 1st line')
print(f'my {a}nd line')
```

## Nesting directives

You can nest directives by ensuring that the ticklines corresponding to the
outermost directive are longer than the ticklines for the inner directives.
For example, nest a warning inside a note block like so:

`````
````{note}
The next info should be nested
```{warning}
Here's my warning
```
````
`````

Here's how it looks rendered:

````{note}
The next info should be nested
```{warning}
Here's my warning
```
````

This can really be abused if you'd like ;-)

``````{note}
The next info should be nested
`````{warning}
Here's my warning
````{admonition} Yep another admonition
```python
# All this fuss was about this boring python?!
print('yep!')
```
````
`````
``````

# Roles - an in-line extension point

Roles are similar to directives - they allow you to define arbitrary new
functionality in Sphinx, but they are use *in-line*. To define an in-line
role, use the following form:

```
{role-name}`role content`
```

For example, the following code:

```
Since Pythagoras, we know that {math}`a^2 + b^2 = c^2`
```

Becomes:

Since Pythagoras, we know that {math}`a^2 + b^2 = c^2`

You can use roles to do things like reference equations and other items in
your book. For example:

````
```{math} e^{i\pi} + 1 = 0
---
label: euler
---
```

Euler's identity, equation {math:numref}`euler`, was elected one of the
most beautiful mathematical formulas.
````

Becomes:

```{math} e^{i\pi} + 1 = 0
---
label: euler
---
```

```{todo}
Figure out why equation referencing didn't work
```
Euler's identity, equation {DOESN'T WORKeq}`euler`, was elected one of the
most beautiful mathematical formulas.
