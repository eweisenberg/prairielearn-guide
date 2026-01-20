---
title: Types of Questions
layout: default
parent: Non-Coding Questions
nav_order: 1
has_toc: false
---

# Types of Questions

You can add the the corresponding HTML tag for the type of question after the `</pl-question-panel>` closing tag. For example, a multiple choice question would have the following general format (replace `<pl-multiple-choice>` with the corresponding HTML tag for the type of question):

```html
<pl-question-panel>
    Question description
</pl-question-panel>

<pl-multiple-choice>
    ...
</pl-multiple-choice>
```

Here are the types of questions you can add:

- [Multiple Choice](multiple-choice.html)
- [Multiselect](multiselect.html)
- [Short Answer](short-answer.html)
- [Matching](matching.html)
- [Order Blocks](order-blocks.html)


All question types support [randomization](randomized-questions.html). You can choose to randomize the question description, answer options, and correct answer(s). You should try to incorporate randomization in your questions if possible.

If you are interested in implementing other types of questions, see the official PrairieLearn documentation [here](https://prairielearn.readthedocs.io/en/latest/elements/).