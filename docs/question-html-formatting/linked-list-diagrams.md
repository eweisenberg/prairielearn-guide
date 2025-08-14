---
title: Linked List Diagrams
layout: default
parent: question.html Formatting
nav_order: 4
---

# Linked List Diagrams

To generate linked list diagrams that look neat and consistent every time, you can use the `<pl-graph>` tag with the GraphViz DOT language. Here is a code template that you can insert into your `question.html` file:  

```html
<div style="float: left;">
<pl-graph>
digraph G {
    rankdir = "LR";
    node [shape = "circle" fontname = "Arial"];
    1 -> 2 -> 3;
}
</pl-graph>
</div>
```

To edit the linked list contents, edit the line containing `1 -> 2 -> 3;` to whatever you'd like you linked list to display. The node names can be any string, but must be enclosed in quotes if they contain spaces. In between each node name should be an arrow.

To make the arrows between the nodes have arrowheads on both ends (to represent a doubly linked list) add the following line below the `node` line within the `<pl-graph>`:

```
edge [dir = "both"];
```

You can change the diagram to be aligned to the center of the question panel by changing `float: left;` to `float: center;`. The purpose of the outer `<div>` tag is to allow aligning the diagram to the left.

The official documentation for GraphViz can be found [here](https://graphviz.org/documentation/).