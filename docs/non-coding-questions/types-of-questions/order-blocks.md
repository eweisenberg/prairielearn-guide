---
title: Order Blocks
layout: default
parent: Types of Questions
nav_order: 5
---

# Order Blocks

Order blocks questions provide a list of options to drag and drop to rearrange in a specific order.

Here is a general template you can use for creating an order blocks question, and what this code is displayed as:

```html
<pl-order-blocks answers-name="ans" grading-method="ranking" source-blocks-order="random" partial-credit="lcs">
  <pl-answer correct="true" ranking="1"><markdown>A</markdown></pl-answer>
  <pl-answer correct="true" ranking="2"><markdown>B</markdown></pl-answer>
  <pl-answer correct="true" ranking="3"><markdown>C</markdown></pl-answer>
</pl-order-blocks>
```

![Image]({{ site.baseurl }}/assets/images/order-blocks-example.png)

By default, using the options in the above template, the order of the answer options is randomized, ranking grading is used, and partial credit is applied. You can add or remove answer options by changing the number of `<pl-answer>` tags within `<pl-order-blocks>`.

Each `<pl-answer>` tag is required to have the attribute `correct`. If you set `correct="false"` for an answer option, then it should not be dragged to the solution box to be marked as correct.

Each `<pl-answer>` tag is also required to have the attribute `ranking`, where the least ranking answer option should be on the top of the solution box. If multiple answer options have the same ranking, then they will be marked as correct in any order.

# Customization

## Arrange solution in a horizontal list

To arrange the order blocks from left to right instead of top to bottom, add the two attributes `inline="true" solution-placement="bottom"` to `<pl-order-blocks>`.

## Set the order of the answer options to appear

Change the `source-blocks-order` attribute in `<pl-order-blocks>` to one of the following options to set the order the answer options appear:

- `source-blocks-order="ordered"` makes the answer options appear in the order that they are in the source `question.html` file.
- `source-blocks-order="alphabetized"` makes the answer options appear in alphabetical order.

<br>

You can read the official PrairieLearn documentation on `<pl-order-blocks>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-order-blocks-element).