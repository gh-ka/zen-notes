---
title: Markdown in 5min
description: 
icon: simple/markdown
status: 
# template: 
hide: 
tags:
  - markdown
cdate: 2026-06-23
mdate:
  - 2026-06-23
  - 2026-06-25-Thu 11:36
---

# Markdown in 5min

## About

- lightweight markup language for authoring text
- created in 2004 by John Gruber, with help from Aaron Swartz
- dialects
  - [Gruber's original](https://daringfireball.net/projects/markdown/)
  - [python-markdown](https://python-markdown.github.io/) with [extensions](https://facelessuser.github.io/pymdown-extensions/)
  - [commonmark](https://commonmark.org/) and  GitHub-flavored Markdown extensions
- [guide](https://www.markdownguide.org/)


## Headers

```md
# H1 Header
## H2 Header
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header
```

## Text formatting

```md
**bold text**
*italic text*
***bold and italic***
~~strikethrough~~
`inline code`
```

## Links and images

```md
[Link text](https://example.com)
[Link with title](https://example.com "Hover title")
![Alt text](image.jpg)
![Image with title](image.jpg "Image title")
```

## Lists

```md
Unordered:

- Item 1
- Item 2
  - Nested item

Ordered:

1. First item
2. Second item
3. Third item
```

## Blockquotes

```md
> This is a blockquote
> Multiple lines
>> Nested quote
```

## Code blocks

````
```javascript
function hello() {
  console.log("Hello, world!");
}
```
````

## Tables

```md
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Row 1    | Data     | Data     |
| Row 2    | Data     | Data     |
```

## Horizontal rule

```md
---
or
***
or
___
```

## Task lists

```md
- [x] Completed task
- [ ] Incomplete task
- [ ] Another task
```

## Escaping characters

```md
Use backslash to escape: \* \_ \# \`
```

## Line breaks

```md
End a line with two spaces  
to create a line break.

Or use a blank line for a new paragraph.
```
