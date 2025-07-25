---
title: Multiline Code Blocks
layout: default
parent: question.html Formatting
nav_order: 2
---

# Multiline Code Blocks

The `<pl-code>` tag can be used to enclose multiline code blocks in a `question.html` file. Here is an example:

```html
<pl-code language="java">public class Node {
    public int val;
    public Node next;

    public Node(int val, Node next) {
        this.val = val;
        this.next = next;
    }
}</pl-code>
```

![Image]({{ site.baseurl }}/assets/images/multiline-code-example.png)

To add line numbers, modify the `<pl-code>` tag like this:

```html
<pl-code language="java" show-line-numbers="true"> ... </pl-code>
```

You can access the official documentation for this question element [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-code-element).