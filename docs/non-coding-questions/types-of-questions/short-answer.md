---
title: Short Answer
layout: default
parent: Types of Questions
nav_order: 3
---

# Short Answer

Short answer questions provide an answer box for students to type in.

Here are general templates you can use for creating a short answer question, and what this code is displayed as:

Integer input:

```html
<pl-integer-input answers-name="ans" placeholder="Type answer here"></pl-integer-input>
```

Floating-point number input:

```html
<pl-number-input answers-name="ans" placeholder="Type answer here"></pl-string-input>
```

String input:

```html
<pl-string-input answers-name="ans" placeholder="Type answer here" remove-leading-trailing="true"></pl-string-input>
```

All are displayed as:

![Image]({{ site.baseurl }}/assets/images/short-answer-example.png)

`<pl-integer-input>` only accepts integer answers, `<pl-number-input>` only accepts floating-point number answers with built in tolerance, and `<pl-string-input>` accepts any type of answer. Therefore, `<pl-string-input>` can be used for integer or number answers as well. Note that nothing should be placed in between the opening and closing tags for each of these input boxes.

All 3 tags are required to have the attribute `answers-name`, and I recommend leaving it as `"ans"` just for simplicity, especially when randomizing questions or adding custom answer parsing. The `placeholder` attribute is optional but recommended for clarity. The `remove-leading-trailing="true"` attribute for `<pl-string-input>` is recommended to remove leading and trailing whitespace from the student's submitted answer before grading (e.g. `" Hello world "` → `"Hello world"`)

To set a single correct answer (checked by basic number/string equality), you need to edit `server.py` for the question and add the following function:

```py
def generate(data):
    data["correct_answers"]["ans"] = x
```

where `x` is replaced by your correct answer in the corresponding data type for the type of input box.

To add custom answer parsing for multiple correct answers or partial credit, edit `server.py` for the question and add the following function:

```py
def grade(data):
    score = 0
    ans = data["submitted_answers"]["ans"] # Student's submitted answer
    
    # Update score to a value between 0.0 and 1.0 based on ans

    data["score"] = score
```

You can use Python string comparison or RegEx to write your custom grading function. `data["score"]` should be set to a value between 0.0 and 1.0 to represent the score the student should receive for their response.

You only need to add one function (either `generate` or `grade`) to `server.py` depending on how you want the question to be graded.

# Customization

## String input ignore case

Add the attribute `ignore-case="true"` to `<pl-string-input>` to disable case sensitivity.

## String input multiline answer

Add the attribute `multiline="true"` to `<pl-string-input>` to allow the student to answer with multiple lines of text.

<br>

You can read the official PrairieLearn documentation on `<pl-integer-input>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-integer-input-element), `<pl-number-input>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-number-input-element), and `<pl-string-input>` [here](https://prairielearn.readthedocs.io/en/latest/elements/#pl-string-input-element).