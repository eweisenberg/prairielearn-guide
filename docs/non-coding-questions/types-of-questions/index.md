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

- [Multiple Choice]({{ site.baseurl }}{% link docs/non-coding-questions/types-of-questions/multiple-choice.md %})
- [Multiselect]({{ site.baseurl }}{% link docs/non-coding-questions/types-of-questions/multiselect.md %})
- [Short Answer]({{ site.baseurl }}{% link docs/non-coding-questions/types-of-questions/short-answer.md %})
- [Matching]({{ site.baseurl }}{% link docs/non-coding-questions/types-of-questions/matching.md %})
- [Order Blocks]({{ site.baseurl }}{% link docs/non-coding-questions/types-of-questions/order-blocks.md %})


All question types support [randomization]({{ site.baseurl }}{% link docs/non-coding-questions/randomized-questions.md %}). You can choose to randomize the question description, answer options, and correct answer(s). You should try to incorporate randomization in your questions if possible.

If you are interested in implementing other types of questions, see the official PrairieLearn documentation [here](https://prairielearn.readthedocs.io/en/latest/elements/).