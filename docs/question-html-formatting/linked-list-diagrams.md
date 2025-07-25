---
title: Linked List Diagrams
layout: default
parent: question.html Formatting
nav_order: 4
---

# Linked List Diagrams

To generate linked list diagrams that look neat and consistent every time, you can use GraphViz with the DOT language. Head over to [this website](https://dreampuf.github.io/GraphvizOnline/?engine=dot#digraph%20G%20%7B%0A%20%20%20%20rankdir%20%3D%20%22LR%22%3B%0A%20%20%20%20node%20%5Bshape%20%3D%20%22circle%22%5D%3B%0A%20%20%20%201%20-%3E%202%20-%3E%203%3B%0A%7D) which contains the following template in the editor pane:

```
digraph G {
    rankdir = "LR";
    node [shape = "circle"];
    1 -> 2 -> 3;
}
```

To edit the linked list contents, edit the line containing `1 -> 2 -> 3;` to whatever you'd like you linked list to display. The node names can be any String, but must be enclosed in quotes if it contains spaces. In between each node name should be an arrow.

To export your UML class diagram, check the "Show raw output" box above the preview pane. Copy the entire SVG HTML code and paste it into your `question.html` file, and you should now see it in the question preview in PrairieLearn!

The official documentation for GraphViz can be found [here](https://graphviz.org/documentation/).