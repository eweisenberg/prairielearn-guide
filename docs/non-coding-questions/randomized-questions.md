---
title: Randomized Questions
layout: default
parent: Non-Coding Questions
nav_order: 2
---

# Randomized Questions

To add randomization to your questions, you will need to modify both `question.html` and `server.py`.

# question.html

PrairieLearn utilizes Mustache in `question.html` files to indicate which text should be randomized. in general, any text enclosed by double curly braces {% raw %}`{{ ... }}`{% endraw %} is replaced by text you have defined in `server.py`. You can find the official Mustache documentation [here](https://mustache.github.io/mustache.5.html).

## Setting a static parameter

Anywhere in `question.html` file, add {% raw %}`{{params.x}}`{% endraw %} where `x` is the name of the parameter. You may have multiple parameters with the same name, or the same parameter multiple times. Parameters can be within the question description, code blocks, answer options, or HTML attributes. To add a full HTML tag that will render properly, use triple curly braces {% raw %}`{{{params.x}}}`{% endraw %} instead.

## Setting a conditional parameter

Use the Mustache tags {% raw %}`{{#params.condition}}`{% endraw %} and {% raw %}`{{/params.condition}}`{% endraw %} where `condition` is the name of the parameter. The text between these tags will only appear if the `condition` parameter is `True` as defined in `server.py`.

## Setting a list of formatted parameters 

Use the Mustache tags {% raw %}`{{#params.list}}`{% endraw %} and {% raw %}`{{/params.list}}`{% endraw %} where `list` is the name of the parameter. The text between these tags should contain the format of the HTML that you would like to be repeated for each element in the list. The randomized parameters within {% raw %}`{{#params.list}}`{% endraw %} and {% raw %}`{{/params.list}}`{% endraw %} should use the format {% raw %}`{{x}}`{% endraw %} where `x` is the name of the parameter (note you do not include `params.` before the name of the parameter).

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

Set `data["params"]["x"]` to the random value of the parameter, where `x` is the name of the parameter you defined in `question.html`. Note that if you are setting an attribute, provide it as a string (e.g. `"true"` instead of `True`). If the parameter is a list, then it should be assigned to a list of dictionaries where each dictionary contains keys as defined by the Mustache tags without the `params.`, and the randomized values you assigned.

# Example

The question `lengthOfCityString` gives the student a string containing the name of a randomly selected city, and they are asked to input the length of that string.

Here is `question.html` for this question:

```html
<pl-question-panel>
    <markdown>Consider the following code:</markdown>
    <pl-code language="java">String city = "{% raw %}{{params.city}}{% endraw %}";</pl-code>
    <markdown>What is `city.length()`?</markdown>
</pl-question-panel>

<pl-integer-input answers-name="ans" placeholder="Type answer here"></pl-integer-input>
```

You can see that the `city` parameter will be randomly generated and inserted into the code block. The randomly generated answer does not need to be included as a Mustache parameter in `question.html` since `pl-integer-input` answers are defined in `server.py`.

Here is `server.py` for this question:

```py
import random

def generate(data):
    cities = ["Tokyo", "New York", "London", "Paris", "Shanghai", "Dubai", "Sydney", "Rome", "Berlin", "Moscow", "Beijing", "Singapore", "Hong Kong", "Seoul", "Madrid", "Toronto", "Mexico City", "Cairo", "Buenos Aires", "Istanbul", "Delhi", "Mumbai", "Jakarta", "Bangkok", "Manila", "Lagos", "Kinshasa", "Dhaka", "Karachi", "Lima", "Bogota", "Santiago", "Kuala Lumpur", "Riyadh", "Tehran", "Baghdad", "Lahore", "Chongqing", "Chennai", "Bengaluru", "Hyderabad", "Osaka", "Nagoya", "Ahmedabad", "Shenzhen", "Guangzhou", "Tianjin", "Chengdu", "Wuhan", "Nanjing", "Hangzhou", "Harbin", "Dalian", "Sapporo", "Busan", "Pyongyang", "Addis Ababa", "Nairobi", "Cape Town", "Alexandria", "Casablanca", "Algiers", "Accra", "Abidjan", "Dakar", "Luanda", "Douala", "Khartoum", "Tunis", "Tripoli", "Damascus", "Amman", "Beirut", "Jerusalem", "Tel Aviv", "Ankara", "Izmir", "Kyiv", "Warsaw", "Prague", "Budapest", "Bucharest", "Vienna", "Lisbon", "Dublin", "Brussels", "Amsterdam", "Copenhagen", "Stockholm", "Oslo", "Helsinki", "Zurich", "Geneva", "Barcelona", "Milan", "Munich", "Hamburg"]
    city = random.choice(cities)
    data["params"]["city"] = city
    data["correct_answers"]["ans"] = len(city)
```

First, I selected one random city from the list of cities. Then, I set `data["params"]["city"]` to this value, and set `data["correct_answers"]["ans"]` to the length of the string, dynamically setting the correct answer. For other types of questions, you may have to edit `data["params"]` instead of `data["correct_answers"]`.

Here is what the question looks like (each student will see a random city):

![Image]({{ site.baseurl }}/assets/images/randomized-example.png)