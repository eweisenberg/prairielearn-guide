---
title: Matching
layout: default
parent: Types of Questions
nav_order: 4
---

# Matching

Matching questions provide a list of statements and options that the student must match each statement to.

Here is a general template you can use for creating a matching question, and what this code is displayed as:

```html
<pl-matching answers-name="ans" counter-type="full-text">
    <pl-statement match="Option 1"><markdown>Statement 1</markdown></pl-statement>
    <pl-statement match="Option 2"><markdown>Statement 2</markdown></pl-statement>
    <pl-statement match="Option 3"><markdown>Statement 3</markdown></pl-statement>
</pl-matching>
```

![Image]({{ site.baseurl }}/assets/images/matching-example.png)

By default, using the options in the above template, the order of the answer options is randomized, all answer choices are shown, and each statement has a drop down where the student can select the correct match out of all options. You can add or remove statements by changing the number of `<pl-statement>` tags within `<pl-matching>`.

Every `<pl-statement>` tag must contain the attribute `match="x"` where `x` is the statement's correct match. Multiple statements can have the same correct match.

# Customization

## Distractor options (options with no matching statements)

Inside the `<pl-matching>` tag, add `<pl-option>` tags in the format `<pl-option>Distractor</pl-option>` and replace `Distractor` with the text of your distractor option.

## List all options next to statements

To list all options next to the statements using keys to map the statements to the options, change the `counter-type` attribute to one of the following:

- `"decimal"` for the options to be labeled 1, 2, 3...
- `"lower-alpha"` for the options to be labeled a, b, c...
- `"upper-alpha"` for the options to be labeled A, B, C...

## Add a "None of the above" option

To add a "None of the above" option to the end of the list of options, add the `none-of-the-above="true"` attribute to `<pl-matching>`

## Only show some of the possible statements

To only show a random subset of possible statements, add the `number-statements="x"` attribute to `<pl-matching>`, where `x` is the number of statements to display.

## Show statements in a fixed order

To show the statements in the order they were written in the source `question.html` file, add the `fixed-order="true"` attribute to `<pl-matching>`.

## Show options in a fixed order

To show the options in the order they were written in the source `question.html` file, add the `fixed-options-order="true"` attribute to `<pl-matching>`. You should explicitly add `<pl-option>` tags for all correct options in the order that you would like them displayed.

<br>

You can read the official PrairieLearn documentation on `<pl-matching>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-matching-element).