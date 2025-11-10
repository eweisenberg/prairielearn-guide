---
title: Tree Diagrams
layout: default
parent: question.html Formatting
nav_order: 5
---

# Tree Diagrams

To generate tree diagrams that look neat and consistent every time, you can use the `<pl-figure>` tag along with a function in `server.py` to dynamically generate the figure. First, copy this code template into your `question.html` file:

```html
<pl-figure file-name="tree.png" type="dynamic" inline="true"></pl-figure>
```

You can modify the `file-name` attribute to whatever you'd like, but remember the name of the file, as we will need it for `server.py`. If you are adding multiple tree diagrams to one question, each `<pl-figure>` tag should have a different `file-name`.

Next, copy the following template into `server.py`. You can leave the `generate(data)` function, if present, before or after the template.

```py
import io
from PIL import Image, ImageDraw, ImageFont

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

def generate_png_image(root):
    """
    Generates the tree as a PIL Image object with anti-aliasing applied.
    """
    positions = calculate_positions(root)
    
    padding = 50
    
    if not positions:
        base_width = padding * 2
        base_height = padding * 2
    else:
        base_width = max(pos[0] for pos in positions.values()) + padding * 2
        base_height = max(pos[1] for pos in positions.values()) + padding * 2

    scale_factor = 2 
    width = base_width * scale_factor
    height = base_height * scale_factor
    
    adjusted_positions = {
        node: (int((pos[0] + padding) * scale_factor), int((pos[1] + padding) * scale_factor)) 
        for node, pos in positions.items()
    }

    img = Image.new('RGB', (int(width), int(height)), 'white')
    draw = ImageDraw.Draw(img)

    try:
        font = ImageFont.truetype("arial.ttf", int(24 * scale_factor * 0.8))
    except IOError:
        font = ImageFont.load_default()

    radius = 20 * scale_factor

    for node, pos in adjusted_positions.items():
        if node.left:
            draw.line([pos, adjusted_positions[node.left]], fill='black', width=int(2 * scale_factor))
        if node.right:
            draw.line([pos, adjusted_positions[node.right]], fill='black', width=int(2 * scale_factor))

    for node, pos in adjusted_positions.items():
        bbox = [pos[0] - radius, pos[1] - radius, pos[0] + radius, pos[1] + radius]
        draw.ellipse(bbox, fill='white', outline='black', width=int(2 * scale_factor))
        
        try:
             draw.text(pos, str(node.value), fill='black', font=font, anchor='mm')
        except AttributeError:
             text_width, text_height = draw.textsize(str(node.value), font)
             text_pos = (pos[0] - text_width / 2, pos[1] - text_height / 2)
             draw.text(text_pos, str(node.value), fill='black', font=font)
            
    img = img.resize((int(base_width), int(base_height)), Image.LANCZOS)
    
    return img

def file(data):
    if data.get("filename") == "tree.png":
        root = TreeNode(5)
        root.left = TreeNode(2)
        root.left.left = TreeNode(1)
        root.left.right = TreeNode(3)
        root.right = TreeNode(9)
        
        img = generate_png_image(root)
        
        img_byte_arr = io.BytesIO()
        img.save(img_byte_arr, format='PNG')
        
        return img_byte_arr.getvalue()

    return b""
```

To ensure the text renders correctly, download [arial.ttf]({{ site.baseurl }}/arial.ttf) and place it in the question folder.

To change the contents of the tree, modify the `file(data)` function's `if` statement to build a binary tree. The `if` statement should check for the file name you specified in `question.html`, and if you have multiple `<pl-figure>` tags, you can add `elif` statements to check for the other file names.

You can access the official documentation for this question element [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-figure-element).