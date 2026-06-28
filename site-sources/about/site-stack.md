---
title: The Tech Stack
description: 
icon: 
status: 
# template: 
hide: 
tags:
  - 
cdate: 2026-06-23-Tue 22:38
mdate:
  - 2026-06-25-Thu 12:08
  - 2026-06-28-Sun 09:57
---

# The Tech Stack and this Repo Evolution

This repo started as a playground on `zensical` and how it can become the replacement for `Material for MkDocs` after the latter hits end of life somewhere this year.

## Change Log

### 2026-06-28-Sun 15:15

- added KaTeX support and [math examples](./markdown/2-md-math.md)

### 2026-06-28-Sun 09:57

- Added example posts [y-z old blog](https://github.com/flyaway1217/ResearchBlog.git) to [here](../yz/index.md)

## Adding upstream

> 2026-06-25-Thu 12:45 created the remote to stop playing for now

```sh
12:40:48 /d/play-zensical (main) $ which gh
/d/_system/ProgramFiles/GitHub CLI/gh

12:40:59 /d/play-zensical (main) $ gh auth status
github.com
  ✓ Logged in to github.com account gh-ka (keyring)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'

12:41:15 /d/play-zensical (main) $  gh repo create zen-notes --private --source=. --remote=upstream --
description 'experiment with zensical for serving markdown notes'
✓ Created repository gh-ka/zen-notes on github.com
  https://github.com/gh-ka/zen-notes
✓ Added remote https://github.com/gh-ka/zen-notes.git

12:43:24 /d/play-zensical (main) $ gh repo list

Showing 19 of 19 repositories in @gh-ka

NAME                             DESCRIPTION                      INFO          UPDATED
gh-ka/zen-notes                  experiment with zensical for...  private       less than a minute ago
gh-ka/md-notes                   markdown notes                   private       about 12 days ago
gh-ka/bash_home                                                   private       about 28 days ago
gh-ka/agent-game                                                  private       about 1 month ago
gh-ka/inference                                                   public        about 1 month ago
gh-ka/cooking                                                     private       about 8 months ago
gh-ka/py_gui                     comparing python gui frameworks  private       about 8 months ago
gh-ka/notes                      Hugo site                        private       about 9 months ago
gh-ka/pyutils                                                     public        about 9 months ago
gh-ka/book-lnx-cmd               track book reading               private       about 9 months ago
gh-ka/pytracer                   A lightweight Python tracing...  public        about 9 months ago
gh-ka/py_dunders                 A runnable 'reference-playgr...  public        about 9 months ago
gh-ka/coding-interview-unive...  A complete computer science ...  public, fork  about 10 months ago
gh-ka/lrn-py-fastapi                                              private       about 1 year ago
gh-ka/whatnot                    Collection of writings - not...  public        about 1 year ago
gh-ka/refcard-org-beamer         Org Beamer reference card        public, fork  about 1 year ago
gh-ka/yt-get-comments            Simple script for downloadin...  public, fork  about 3 years ago
gh-ka/pythonaday_parsing         Forked following yt video se...  public, fork  about 4 years ago
gh-ka/dot-emacs-d                                                 public        about 5 years ago

12:43:32 /d/play-zensical (main) $ git rv
upstream        https://github.com/gh-ka/zen-notes.git (fetch)
upstream        https://github.com/gh-ka/zen-notes.git (push)
```

## Basics

Started following the docs and quickly created the basic new site.

> **Create python project**

```sh
22:32:58 /d $ which uv
/d/_system/gitbash_home/.local/bin/uv

22:33:17 /d $ mkdir play-zensical

22:33:47 /d $ cd play-zensical/

22:33:57 /d/play-zensical $ uv init
Initialized project `play-zensical`

22:34:05 /d/play-zensical $ ll
total 12
drwxr-xr-x 1 kathy 197121   0 Jun 23 22:33 ../
-rw-r--r-- 1 kathy 197121 109 Jun 23 22:34 .gitignore
-rw-r--r-- 1 kathy 197121 159 Jun 23 22:34 pyproject.toml
-rw-r--r-- 1 kathy 197121  91 Jun 23 22:34 main.py
-rw-r--r-- 1 kathy 197121   5 Jun 23 22:34 .python-version
-rw-r--r-- 1 kathy 197121   0 Jun 23 22:34 README.md
drwxr-xr-x 1 kathy 197121   0 Jun 23 22:34 ./
drwxr-xr-x 1 kathy 197121   0 Jun 23 22:34 .git/

22:35:26 /d/play-zensical $ uv run main.py
Hello from play-zensical!
```

> **Add zensical to the project**

```sh
22:36:06 /d/play-zensical $ uv add --dev zensical
Resolved 12 packages in 1.72s
Prepared 10 packages in 1m 43s
░░░░░░░░░░░░░░░░░░░░ [0/11] Installing wheels...                                                      warning: Failed to hardlink files; falling back to full copy. This may lead to degraded performance.
         If the cache and target directories are on different filesystems, hardlinking may not be supported.
         If this is intentional, set `export UV_LINK_MODE=copy` or use `--link-mode=copy` to suppress this warning.
Installed 11 packages in 38.63s
 + click==8.4.1
 + colorama==0.4.6
 + deepmerge==2.1.0
 + jinja2==3.1.6
 + markdown==3.10.2
 + markupsafe==3.0.3
 + pygments==2.20.0
 + pymdown-extensions==11.0
 + pyyaml==6.0.3
 + tomli==2.4.1
 + zensical==0.0.46

 22:39:34 /d/play-zensical $ uv pip list
Package            Version
------------------ -------
click              8.4.1
colorama           0.4.6
deepmerge          2.1.0
jinja2             3.1.6
markdown           3.10.2
markupsafe         3.0.3
pygments           2.20.0
pymdown-extensions 11.0
pyyaml             6.0.3
tomli              2.4.1
zensical           0.0.46

22:39:38 /d/play-zensical $ uv run zensical
Usage: zensical [OPTIONS] COMMAND [ARGS]...

  Zensical - A modern static site generator.

Options:
  --version  Show the version and exit.
  --help     Show this message and exit.

Commands:
  build  Build a project.
  new    Create a new template project in the current or given directory.
  serve  Build and serve a project.
```

> **Create zensical project**

```sh
22:40:06 /d/play-zensical $ uv run zensical new

22:41:04 /d/play-zensical $ ll
total 84
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:33 ../
-rw-r--r-- 1 kathy 197121   109 Jun 23 22:34 .gitignore         # updated
-rw-r--r-- 1 kathy 197121    91 Jun 23 22:34 main.py
-rw-r--r-- 1 kathy 197121     5 Jun 23 22:34 .python-version
-rw-r--r-- 1 kathy 197121     0 Jun 23 22:34 README.md
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:35 .venv/
-rw-r--r-- 1 kathy 197121   214 Jun 23 22:36 pyproject.toml
-rw-r--r-- 1 kathy 197121 52884 Jun 23 22:36 uv.lock
-rw-r--r-- 1 kathy 197121 15192 Jun 23 22:41 zensical.toml       # added
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:41 docs/               # added
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:41 .github/            # added
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:41 ./
drwxr-xr-x 1 kathy 197121     0 Jun 23 22:41 .git/

22:45:26 /d/play-zensical $ uv run zensical serve
Serving \\?\D:\play-zensical\site on http://localhost:8000
Build started
No issues found
No issues found
```

At this point, the basic site with `zensical` and `markdown` guides is up and running on `http://localhost:8000`

## Deeper In

- Turns out the functionality is still very basic although some of the "strange" features I've experienced before are still around
- Major deficiencied
  - **Configuration/flexibitity**. In general, hard to get config right - some of the tweaks are counter intuitive. In particular:
    - Navigation is all or nothing so you either list all the entries OR you leave it out and then it picks up everything
  - **Server refresh** does not seem to pick up everything so at times I had to stop the server, delete the site and restart to see the effect
  - **Functionality/plugins**. Core functionality is rather limited, plugins are not yet implemented.
    - blog
    - tags
    - dates

## Achieved

Two days of tweaking brought me to customizing the default site to:

- including several sections with bearable implicit navigation
- changing the icon/flavicon
- improved `zensical` and `markdown` guides
- adding creation and modification dates to be displayed
- finally creating the vscode frontmatter snippet !!!

## Findings

After two days fooling around, discovered

- Zensical's own [docs](https://github.com/zensical/docs) use `mkdocs.yaml` and do not seem to include automation
- An [additional project working on rejuvinating the `Material for MkDocs`](https://materialx.org/)
  - [blogs support](https://jaywhj.github.io/mkdocs-materialx/tutorials/blogs/basic.html)
- An AI-generated project someone put together to reproduce [blog plugin](https://github.com/knu2xs/zensical-blog)
- Quite a few sites already using `zensical`
  - this all has started after discovering the [beancount docs site](https://github.com/beancount/docs) 😄
  - https://github.com/nicholaswilde/cook-docs  (scripted)
  - https://github.com/nicholaswilde/recipes (scripted)
  - https://github.com/nicholaswilde/gardening (scripted)
  - https://github.com/nicholaswilde/notes (manual)

## Questions and TODOs

- still not sure about customization - icons, styles, scripts, etc
- discovered that many new project are heavily AI driven and i do not fully understand the workflow; would be good to get back there especially as the chat gets more and more frustrating with time
- automation to get the functionality i need
- *most important* - I still do not seem to know what to write and what to publish if at all
- how to create index of pages with brief summary as in some blogs (without manual editing)
- how to refer to external files

```sh
Warning: page does not exist
    ╭─[ index.md:23:20 ]
    │
 23 │ 1. Repo [`README`](../README.md) summarizing the experience
    │                    ──────┬─────
    │                          ╰─────── page does not exist
```

- how to use icons from other projects to add to pages, e.g. that of `zensical`
