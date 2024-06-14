---
title: "Markdown Syntax"
date: 2023-11-20
layout: post
author: jeevan
image: "assets/images/banner/markdown.jpg"
categories: [Markdown, tutorial]
---

Guide to streamlined text formatting. Learn the basics and unleash the power of clean and simple document styling with Markdown.

## Headings

Commonly Used

```
# A first-level heading - H1
## A second-level heading - H2
### A third-level heading - H3
```

Infrequently Used

```
#### A fourth-level heading - H4
##### A fifth-level heading - H5
###### A sixth-level heading - H6
```

## Emphasis Text

Bold: **Bold** <br>
Italic: _Italic_ <br>
Strike Off: ~~Strike Off~~ <br>
Subscript: This is a <sub>subscript</sub> text <br>
Superscript: This is a <sup>superscript</sup> text

## Blockquote

> Text that is a quote

With other elements

> ### The quarterly results look great!
>
> - Revenue was off the chart.
> - Profits were higher than ever.
>
>   _Everything_ is going according to **plan**.

## Horizontal line

---

## Highlight

I need to highlight these ==very important words==.

## Custom Heading

### My Great Heading {#custom-id}

## Code Block

Code block

`single line`

Code block - Multiple lines

```python
# Python
a = 1
b = 2
```

Language Specific

```json
# Json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

## Links

This is a sample [link](https://www.example.com)

## Images

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://myoctocat.com/assets/images/base-octocat.svg)

## Lists

Unordered List

- apple
- orange

Ordered List

1. apple
1. orange

Nested List

1. First list item
   - First nested list item
     - Second nested list item

## Tasks

- [ ] apple
- [x] orange
  - [ ] apple

## Goto Statement/References

The **go to** statement should be abolished [[1]](#references).

## Mention People

@github/support What do you think about these updates?

## Emojis

@octocat :+1: This PR looks great - it's ready to merge! :shipit: :joy:

For a full list of available emoji and codes, see the [Emoji-Cheat-Sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md).

## Comment

```
<!-- This content will not appear in the rendered Markdown -->
```

## Table

Normal Table without alignment

| Column 1 | Column 2 |
| :------- | :------- |
| Cell 1   | Cell 2   |
| Cell 1   | Cell 2   |

Table with Alignment

| Syntax    | Description |   Test Text |
| :-------- | :---------: | ----------: |
| Header    |    Title    | Here's this |
| Paragraph |    Text     |    And more |

## Acknowledgments

Use this space to list resources you find helpful and would like to give credit to. I've included a few of my favorites to kick things off!

- [Choose an Open Source License](https://choosealicense.com)
- [GitHub Pages](https://pages.github.com)

## References

[1] [Basic Syntax](https://www.markdownguide.org/basic-syntax/)

[2] [Extended Syntax](https://www.markdownguide.org/extended-syntax/)

[3] [Github official docs](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#section-links)
