---
title: Zensical in 5min
description: 
icon: lucide/rocket
status: 
# template: 
hide: 
tags:
  - 
cdate: 2026-06-23
mdate:
  - 2026-06-24
  - 2026-06-25-Thu 11:39
---

# Zensical in 5min

- modern static site generator
- by the creators of Material for MkDocs
- written in Rust and Python
- published as a [Python package](https://pypi.org/project/zensical)
- [documentation](https://zensical.org/docs/)
- [code repo](https://github.com/zensical/zensical)
- [docs repo](https://github.com/zensical/docs)

## Installation and Usage

```sh
# make uv is available, create python project in a new folder
uv init     

# get project depend on zensical
uv add --dev zensical

# get zensical create a new documentation project
uv run zensical new

# explore the site generated and rendered by default
uv run zensical serve

# build your project
uv run zensical build
```

## Configuration

- `zensical.toml` but can also use the legacy `mkdocs.yml`

```toml
[project]
site_name = "My Zensical project"
site_url = "https://example.com
site_description = "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
site_author = "John Doe"
copyright = "&copy; 2025 Jane Doe"

# source files directory
docs_dir = "docs"
# generated site directory
site_dir = "site"

# controls the directory structure ?
use_directory_urls = false

# address used by serve command
dev_addr = "localhost:3000"

# additional files to watch
watch = ["data.csv", "fragments"]

# links color
palette.primary = "lime"

[project.theme]
# classic` to mimic Material for MkDocs, `modern` for zensical default
variant = "modern"

[project.extra]
# extra key-value pairs used by templates
key = "value"
```

## Authoring

- use relative md-style page links (good for migration) and not html-style links (good for potential non-html rendering)
- page title comes from:
  1. `nav` config;
  2. frontmatter;
  3. `#`;
  4. file name
- frontmatter
  - `title`
  - `description`
  - `icon`, from the [included icon sets](https://zensical.org/docs/authoring/icons-emojis/#included-icon-sets)
  - `status`, can be `new`, `depricated` or as defined by `[project.extra.status]`
  - `template` file in `overrides` directory, default is `main.html`
  - `hide` list of elements to hide, e.g., `navigation` and `toc`
  - can be added through templates

## Examples

### Admonitions

> Go to [documentation](https://zensical.org/docs/authoring/admonitions/)

!!! note

    This is a **note*&- admonition. Use it to provide helpful information.

!!! warning

    This is a **warning** admonition. Be careful!

#### Details

> Go to [documentation](https://zensical.org/docs/authoring/admonitions/#collapsible-blocks)

??? info "Click to expand for more info"

    This content is hidden until you click to expand it.
    Great for FAQs or long explanations.

### Code Blocks

> Go to [documentation](https://zensical.org/docs/authoring/code-blocks/)

``` python hl_lines="2" title="Code blocks"
def greet(name):
    print(f"Hello, {name}!") # (1)!

greet("Python")
```

1.  > Go to [documentation](https://zensical.org/docs/authoring/code-blocks/#code-annotations)

    Code annotations allow to attach notes to lines of code.

Code can also be highlighted inline: `#!python print("Hello, Python!")`.

### Content tabs

> Go to [documentation](https://zensical.org/docs/authoring/content-tabs/)

=== "Python"

    ``` python
    print("Hello from Python!")
    ```

=== "Rust"

    ``` rs
    println!("Hello from Rust!");
    ```

### Diagrams

> Go to [documentation](https://zensical.org/docs/authoring/diagrams/)

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

### Footnotes

> Go to [documentation](https://zensical.org/docs/authoring/footnotes/)

Here's a sentence with a footnote.[^1]

Hover it, to see a tooltip.

[^1]: This is the footnote.


### Formatting

> Go to [documentation](https://zensical.org/docs/authoring/formatting/)

- ==This was marked (highlight)==
- ^^This was inserted (underline)^^
- ~~This was deleted (strikethrough)~~
- H~2~O
- A^T^A
- ++ctrl+alt+del++

### Icons, Emojis

> Go to [documentation](https://zensical.org/docs/authoring/icons-emojis/)

- :sparkles: `:sparkles:`
- :rocket: `:rocket:`
- :tada: `:tada:`
- :memo: `:memo:`
- :eyes: `:eyes:`

### Maths

> Go to [documentation](https://zensical.org/docs/authoring/math/)

$$
\cos x=\sum_{k=0}^{\infty}\frac{(-1)^k}{(2k)!}x^{2k}
$$

!!! warning "Needs configuration"
    Note that MathJax is included via a `script` tag on this page and is not
    configured in the generated default configuration to avoid including it
    in a pages that do not need it. See the documentation for details on how
    to configure it on all your pages if they are more Maths-heavy than these
    simple starter pages.

<script id="MathJax-script" src="https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js"></script>
<script>
  window.MathJax = {
    tex: {
      inlineMath: [["\\(", "\\)"]],
      displayMath: [["\\[", "\\]"]],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      ignoreHtmlClass: ".*|",
      processHtmlClass: "arithmatex"
    }
  };

  document$.subscribe(() => {
    MathJax.startup.output.clearCache()
    MathJax.typesetClear()
    MathJax.texReset()
    MathJax.typesetPromise()
  })
</script>

### Task Lists

> Go to [documentation](https://zensical.org/docs/authoring/lists/#using-task-lists)

- [x] Install Zensical
- [x] Configure `zensical.toml`
- [x] Write amazing documentation
- [ ] Deploy anywhere

### Tooltips

> Go to [documentation](https://zensical.org/docs/authoring/tooltips/)

[Hover me][example]

  [example]: https://example.com "I'm a tooltip!"
