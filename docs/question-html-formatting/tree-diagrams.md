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

The offical documentation for this question element can be found [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-figure-element).