---
title: 
description: 
icon: 
status: 
# template: 
hide: 
tags:
  - 
cdate: 2026-06-23-Tue 22:38
mdate:
  - 2026-06-25-Thu 12:12
---

# README

This is a testing playground to experimenting with `zensical`.

## Usage

To use this repo as is, you need to have `python` and `uv` available on your computer.

```sh
which python
which uv
```

1. Clone the repo

```sh
git clone <repo-url> <local-repo-name>
cd <local-repo-name>
```

1. Recreate virtual environment

```sh
uv sync
```

1. Run zensical to serve the site locally

```sh
uv run zensical serve
```

1. If all is ok, you point your browser to [the local zensical server](http://localhost:8000/) and observe the contents.

1. Tweak whatever you like - configuration, contents, structure - to make it your own if you like!
