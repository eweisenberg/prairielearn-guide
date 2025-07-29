---
title: Randomized Questions
layout: default
parent: Non-Coding Questions
nav_order: 2
---

# Randomized Questions

To add randomization to your questions, you will need to modify both `question.html` and `server.py`.

# question.html

PrairieLearn utilizes Mustache in `question.html` files to indicate which text should be randomized. in general, any text enclosed by double curly braces `{{ ... }}` is replaced by text you have defined in `server.py`. You can find the official Mustache documentation [here](https://mustache.github.io/mustache.5.html).

## Setting a static parameter

Anywhere in `question.html` file, add `{{params.x}}` where `x` is the name of the parameter. You may have multiple parameters with the same name, or the same parameter multiple times. Parameters can be within the question description, code blocks, answer options, or HTML attributes. To add a full HTML tag that will render properly, use triple curly braces `{{{params.x}}}` instead.

## Setting a conditional parameter

Use the Mustache tags `{{#params.condition}}` and `{{/params.condition}}` where `condition` is the name of the parameter. The text between these tags will only appear if the `condition` parameter is `True` as defined in `server.py`.

## Setting a list of formatted parameters 

Use the Mustache tags `{{#params.list}}` and `{{/params.list}}` where `list` is the name of the parameter. The text between these tags should contain the format of the HTML that you would like to be repeated for each element in the list. The randomized parameters within `{{#params.list}}` and `{{/params.list}}` should use the format `{{x}}` where `x` is the name of the parameter (note you do not include `params.` before the name of the parameter).

# server.py

`server.py` should have this general format:

```py
import random

def generate(data):
    # Generate random values first
    # Then set data["params"] to their randomized value
```

## Generate random values

### Random integer

Use `x = random.randint(i, j)` to generate a random integer `i <= x <= j`.

### Random floating-point number

Use `x = random.random()` to generate a random float `0 <= x < 1`. You can use arithmetic to modify this value to change the range.

### Random element from list

Use `x = random.choice(list)` to set `x` to a random element from `list`. For example, `random.choice(["A", "B", "C"])` will return either `"A"`, `"B"`, or `"C"`.

### Random set of elements from list

Use `x = random.sample(list, k)` to set `x` to a list of `k` random elements from `list`. For example, `random.choice(range(1, 11), 4)` will return a list of 4 random unique integers between 1 and 10, inclusive.

## Set data["params"]

Set `data["params"]["x"]` to the random value of the parameter, where `x` is the name of the parameter you defined in `question.html`. If the parameter is a list, then it should be assigned to a list of dictionaries where each dictionary contains keys as defined by the Mustache tags without the `params.`, and the randomized values you assigned.