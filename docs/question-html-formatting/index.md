---
title: question.html Formatting
layout: default
nav_order: 5
has_toc: false
---

# question.html Formatting

This section contains various guides to format questions in a consistent manner that makes them more readable and understandable. The following guides can be applied to any question's `question.html` file for easy formatting. All of the following elements should be placed inside the `<pl-question-panel>` tag.

- [Markdown]({{ site.baseurl }}{% link docs/question-html-formatting/markdown.md %})
- [Multiline Code Blocks]({{ site.baseurl }}{% link docs/question-html-formatting/multiline-code-blocks.md %})
- [UML Class Diagrams]({{ site.baseurl }}{% link docs/question-html-formatting/uml-class-diagrams.md %})
- [Linked List Diagrams]({{ site.baseurl }}{% link docs/question-html-formatting/linked-list-diagrams.md %})


Note that within any of these elements, if you want to render any of the following symbols, you should convert them to the following codes to not break the HTML:

`<` → `&lt;`

`>` → `&gt;`

`&` → `&amp;`

For example, to properly render the text `List<Integer>`, you should convert it to `List&lt;Integer&gt;` in `question.html`.

[Here](https://www.textfixer.com/html/html-character-encoding.php) is a useful website that can do the conversion for you.