---
title: Tree Diagrams
layout: default
parent: question.html Formatting
nav_order: 5
---

# Tree Diagrams

To generate tree diagrams that look neat and consistent every time, you can use the `<pl-figure>` tag along with a function in `server.py` to dynamically generate the figure. First, copy this code template into your `question.html` file:

```html
<pl-figure file-name="tree.svg" type="dynamic" inline="true"></pl-figure>
```

You can modify the `file-name` attribute to whatever you'd like, but remember the name of the file, as we will need it for `server.py`. If you are adding multiple tree diagrams to one question, each `<pl-figure>` tag should have a different `file-name`.

Next, copy the following template into `server.py`. You can leave the `generate(data)` function, if present, before or after the template.

```py
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def calculate_positions(root, x=0, y=0, x_offset=40, y_offset=60):
    positions = {}
    
    def _traverse(node, x, y):
        if not node:
            return x
        x = _traverse(node.left, x, y + y_offset)
        positions[node] = (x, y)
        x += x_offset
        x = _traverse(node.right, x, y + y_offset)
        return x

    _traverse(root, x, y)
    return positions

def generate_svg_content(root):
    """
    Generates the SVG content for the tree as a string.
    """
    positions = calculate_positions(root)
    
    # Add padding to prevent cropping
    padding = 50
    width = max(pos[0] for pos in positions.values()) + padding * 2
    height = max(pos[1] for pos in positions.values()) + padding * 2
    
    # Adjust all positions by padding to center the drawing
    adjusted_positions = {node: (pos[0] + padding, pos[1] + padding) for node, pos in positions.items()}
    
    svg_content = [
        f'<svg width="{width}" height="{height}" xmlns="http://www.w3.org/2000/svg">\n'
    ]
    
    # Draw lines connecting parent to children using adjusted positions
    for node, pos in adjusted_positions.items():
        if node.left:
            svg_content.append(f'<line x1="{pos[0]}" y1="{pos[1]}" x2="{adjusted_positions[node.left][0]}" y2="{adjusted_positions[node.left][1]}" stroke="black" stroke-width="2" />\n')
        if node.right:
            svg_content.append(f'<line x1="{pos[0]}" y1="{pos[1]}" x2="{adjusted_positions[node.right][0]}" y2="{adjusted_positions[node.right][1]}" stroke="black" stroke-width="2" />\n')
    
    # Draw the nodes as white circles with black text using adjusted positions
    for node, pos in adjusted_positions.items():
        svg_content.append(f'<circle cx="{pos[0]}" cy="{pos[1]}" r="20" fill="white" stroke="black" stroke-width="2" />\n')
        svg_content.append(f'<text x="{pos[0]}" y="{pos[1]+5}" text-anchor="middle" font-size="16" font-family="Arial">{node.value}</text>\n')
        
    svg_content.append('</svg>')
    
    return "".join(svg_content)

def file(data):
    """
    Returns the generated SVG content as a bytes-like object.
    """
    if data.get("filename") == "tree.svg":
        root = TreeNode(5)
        root.left = TreeNode(2)
        root.left.left = TreeNode(1)
        root.left.right = TreeNode(3)
        root.right = TreeNode(9)
        
        svg_string = generate_svg_content(root)
        
        return svg_string.encode('utf-8')

    return ""
```

To change the contents of the tree, modify the `file(data)` function's `if` statement to build a binary tree. The `if` statement should check for the file name you specified in `question.html`, and if you have multiple `<pl-figure>` tags, you can add `elif` statements to check for the other file names.

You can access the official documentation for this question element [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-figure-element).