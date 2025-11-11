---
title: Tree Diagrams
layout: default
parent: question.html Formatting
nav_order: 5
---

# Tree Diagrams

To generate tree diagrams that look neat and consistent every time, you can use the following online Jupyter notebook: [binary-tree-visualizer](https://eweisenberg.github.io/binary-tree-visualizer/lab/index.html).

Open `tree_visualizer.ipynb` and run the first large cell with code. Scroll down to the second code cell and modify the code to create the desired tree (sample code provided to show syntax). Next, run both the second code cell and third code cell to generate the image. It should now appear in the file browser on the left, where you can right click and Download.

Inside the question folder, create a new folder called `clientFilesQuestion` if it does not already exist. Place the image into `clientFilesQuestion`, and insert this template into `question.html`, replacing `imagename.png` with the name of the image file and filling in the alt text:

```html
<pl-figure
  file-name="imagename.png"
  alt="alt text"
></pl-figure>
```

JupyterLite saves your code modifications in the browser cache. If you accidentally break the code or want to revert to the original, go into your browser settings and clear the site data for `eweisenberg.github.io`.

The original three code cells are also provided here if you would like to copy and paste them:

```py
import io
from PIL import Image, ImageDraw, ImageFont

class TreeNode:
    """
    Represents a single node in a binary tree.
    Includes an optional 'color' parameter for visualization.
    """
    def __init__(self, value, color="white"):
        self.value = value
        self.left = None
        self.right = None
        self.color = color

def calculate_positions(root, x=0, y=0, x_offset=40, y_offset=60):
    """
    Calculates the (x, y) position for each node using an in-order traversal
    to ensure nodes do not overlap horizontally.
    """
    positions = {}
    
    def _traverse(node, x, y):
        if not node:
            return x
        
        # Traverse left subtree
        x = _traverse(node.left, x, y + y_offset)
        
        # Position current node
        positions[node] = (x, y)
        x += x_offset  # Move x to the right for the next node
        
        # Traverse right subtree
        x = _traverse(node.right, x, y + y_offset)
        
        return x

    # Start traversal and correct the initial x-positioning
    max_x = _traverse(root, x, y)
    
    # Center the tree horizontally
    min_x = min(pos[0] for pos in positions.values()) if positions else 0
    center_offset = (0 - min_x) + x_offset 
    
    # Re-adjust positions for centering
    final_positions = {
        node: (pos[0] + center_offset, pos[1])
        for node, pos in positions.items()
    }
    
    return final_positions

def generate_png_image(root):
    """
    Generates the tree as a PIL Image object with anti-aliasing applied via scaling.
    """
    positions = calculate_positions(root)
    
    padding = 50
    
    if not positions:
        base_width = padding * 2
        base_height = padding * 2
    else:
        # Determine base size
        max_x = max(pos[0] for pos in positions.values())
        min_x = min(pos[0] for pos in positions.values())
        max_y = max(pos[1] for pos in positions.values())
        
        base_width = (max_x - min_x) + padding * 2 + 40 # Add extra buffer
        base_height = max_y + padding * 2

    scale_factor = 4 # High scale factor for better anti-aliasing
    width = base_width * scale_factor
    height = base_height * scale_factor
    
    # Calculate offset to handle nodes starting at min_x > 0
    x_offset_for_centering = padding - min_x if positions else padding

    adjusted_positions = {
        node: (int((pos[0] + x_offset_for_centering) * scale_factor), 
               int((pos[1] + padding) * scale_factor))
        for node, pos in positions.items()
    }

    img = Image.new('RGB', (int(width), int(height)), 'white')
    draw = ImageDraw.Draw(img)

    try:
        # Try a common font, otherwise fall back to default
        font = ImageFont.truetype("arial.ttf", int(24 * scale_factor * 0.8))
    except IOError:
        font = ImageFont.load_default()

    radius = 20 * scale_factor
    line_width = int(2 * scale_factor)

    # 1. Draw connecting lines
    for node, pos in adjusted_positions.items():
        if node.left:
            draw.line([pos, adjusted_positions[node.left]], fill='black', width=line_width)
        if node.right:
            draw.line([pos, adjusted_positions[node.right]], fill='black', width=line_width)

    # 2. Draw nodes and text
    for node, pos in adjusted_positions.items():
        
        # --- Dynamic Color Logic ---
        node_color = node.color.lower()
        if node_color == "red":
            fill_color = 'red'
            text_color = 'white'
            outline_color = 'black'
        elif node_color == "black":
            fill_color = 'black'
            text_color = 'white'
            outline_color = 'black' 
        else:
            fill_color = 'white'
            text_color = 'black'
            outline_color = 'black'
        # ---------------------------

        # Draw circle
        bbox = [pos[0] - radius, pos[1] - radius, pos[0] + radius, pos[1] + radius]
        draw.ellipse(bbox, fill=fill_color, outline=outline_color, width=line_width)
        
        # Draw text (using 'mm' anchor for perfect centering in modern PIL)
        try:
             draw.text(pos, str(node.value), fill=text_color, font=font, anchor='mm')
        except AttributeError:
             # Fallback for older PIL versions
             text_width, text_height = draw.textsize(str(node.value), font)
             text_pos = (pos[0] - text_width / 2, pos[1] - text_height / 2)
             draw.text(text_pos, str(node.value), fill=text_color, font=font)
             
    # Scale down using high-quality resampling (LANCZOS for anti-aliasing)
    img = img.resize((int(base_width), int(base_height)), Image.LANCZOS)
    
    return img
```

```py
# White by default, add second parameter for red or black
root = TreeNode(5)
root.left = TreeNode(2)
root.left.left = TreeNode(1)
root.left.right = TreeNode(3, "red")
root.right = TreeNode(9, "black")
```

```py
img = generate_png_image(root)
img.save("tree.png", "PNG")
```

The offical documentation for this question element can be found [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-figure-element).