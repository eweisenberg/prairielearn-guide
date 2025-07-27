---
title: Multiselect
layout: default
parent: Types of Questions
nav_order: 2
---

# Multiselect

Multiselect (checkbox) questions provide a list of answer choice options where multiple options may be correct.

Here is a general template you can use for creating a multiselect question, and what this code is displayed as:

```html
<pl-checkbox answers-name="ans" hide-letter-keys="true" number-answers="4" min-correct="1" max-correct="4" partial-credit="true" partial-credit-method="EDC">
    <pl-answer correct="true"><markdown>Option 1</markdown></pl-answer>
    <pl-answer correct="true"><markdown>Option 2</markdown></pl-answer>
    <pl-answer correct="true"><markdown>Option 3</markdown></pl-answer>
    <pl-answer correct="false"><markdown>Option 4</markdown></pl-answer>
    <pl-answer correct="false"><markdown>Option 5</markdown></pl-answer>
    <pl-answer correct="false"><markdown>Option 6</markdown></pl-answer>
</pl-checkbox>
```

![Image]({{ site.baseurl }}/assets/images/multiselect-example.png)

By default, using the options in the above template, the order of the answer options is randomized, the letter keys (A, B, C, D, ...) are not shown, and partial credit will be given.

The total number of options displayed is set by the attribute `number-answers`. The minimum number of correct answer options that will be *shown* is set by `min-correct`, and the maximum number of correct answer options *shown* is set by `max-correct`. I recommend leaving `min-correct` as 1 and `max-correct` as the number of answers displayed. Also, having more answer options than the number of answers displayed is a simple way to introduce randomization into your question without any additional code. To limit the number of answer options that can be *selected* (e.g. Select exactly 2 options), see the Customization section below.

The `<pl-checkbox>` tag is required to have the attribute `answers-name`, and I recommend leaving it as `"ans"` just for simplicity, especially when randomizing questions. The `hide-letter-keys` attribute is optional but recommended since students don't need to see the letter keys for an online exam without a physical bubble sheet.

Each `<pl-answer>` may have `correct="true"`, and there should be multiple answer options with this attribute. For incorrect answer options, the default value is `correct="false"`, but you can add that attribute for clarity if you'd like.

# Customization

## Set the order of the answer choices to appear

Add the attribute `fixed-order="true"` to the `<pl-checkbox>` tag to make the answer options appear in the order they are in the source `question.html` file. This is not recommended if you list all the correct answers first and all the incorrect answers afterwards in `question.html`.

## Limit the number of answers that can be selected

Add the attribute `min-select="x"` where `x` is the minimum number of answer options that must be selected for a valid submission, and add the attribute `max-select="y"` where `y` is the maximum number of answer options that must be selected for a valid submission. If the student should select exactly a certain number of answers, use the same number for both `min-select` and `max-select`.