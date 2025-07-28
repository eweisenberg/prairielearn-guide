---
title: Multiple Choice
layout: default
parent: Types of Questions
nav_order: 1
---

# Multiple Choice

Multiple choice questions provide a list of answer choice options where only one option is correct.

Here is a general template you can use for creating a multiple choice question, and what this code is displayed as:

```html
<pl-multiple-choice answers-name="ans" hide-letter-keys="true">
    <pl-answer correct="true"><markdown>Option 1</markdown></pl-answer>
    <pl-answer><markdown>Option 2</markdown></pl-answer>
    <pl-answer><markdown>Option 3</markdown></pl-answer>
    <pl-answer><markdown>Option 4</markdown></pl-answer>
    <pl-answer><markdown>Option 5</markdown></pl-answer>
</pl-multiple-choice>
```

![Image]({{ site.baseurl }}/assets/images/multiple-choice-example.png)

By default, using the options in the above template, the order of the answer options is randomized, all answer choices are shown, and the letter keys (A, B, C, D, ...) are not shown. You can add or remove answer options by changing the number of `<pl-answer>` tags within `<pl-multiple-choice>` (e.g. a true/false question would only have 2 `<pl-answer>` tags).

The `<pl-multiple-choice>` tag is required to have the attribute `answers-name`, and I recommend leaving it as `"ans"` just for simplicity, especially when randomizing questions. The `hide-letter-keys` attribute is optional but recommended since students don't need to see the letter keys for an online exam without a physical bubble sheet.

One `<pl-answer>` tag is required to have the attribute `correct="true"`. If you add multiple answer options with `correct="true"`, then only one correct answer option will be shown at random. For incorrect answer options, the default value is `correct="false"`, but you can add that attribute for clarity if you'd like.

# Customization

## Set the order of the answer choices to appear

Add one of the following attributes to `<pl-multiple-choice>` to set the order the answer choices appear:

- `order="fixed"` makes the answer options appear in the order that they are in the source `question.html` file.
- `order="ascend"` or `order="descend"` makes the answer options appear in ascending or descending alphabetical order.

Avoid using this feature unless it is needed to make the question more clear, or the answer options are already randomly generated, as it makes it easier for students to copy off of each other's screens.

## Add "All of the above" or "None of the above" options

Add the attribute `all-of-the-above="correct"` or `all-of-the-above="incorrect"` to `<pl-multiple-choice>` to add an "All of the above" option that will always be shown as the last option, with the other options in randomized order. Choose "correct" if "All of the above" is the correct answer, and "incorrect" if it is an incorrect answer (distractor option).

To add a "None of the above" option, use the same rules as above except with `none-of-the-above` instead of `all-of-the-above`. It is possible to have both `none-of-the-above` and `all-of-the-above` in the same question.

## Only show some of the possible answer choices

Add the attribute `number-answers="x"` and replace `x` with the number of answers to be displayed. One correct answer will always be displayed, and the rest will be incorrect.

<br>

You can read the official PrairieLearn documentation on `<pl-multiple-choice>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-multiple-choice-element).