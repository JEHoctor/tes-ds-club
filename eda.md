# Coding + Statistics = EDA

Here is a function that downloads the iris flowers dataset from the website of the University of California, Irvine (UCI).
Copy this function and run it with `load_iris()`.
What does the output look like?

```python
!pip install ucimlrepo
from ucimlrepo import fetch_ucirepo
def load_iris():
    iris = fetch_ucirepo(id=53)
    X = iris.data.features
    sepal_length = X["sepal length"].tolist()
    sepal_width = X["sepal width"].tolist()
    petal_length = X["petal length"].tolist()
    petal_width = X["petal width"].tolist()
    y = iris.data.targets["class"].tolist()
    return sepal_length, sepal_width, petal_length, petal_width, y
```

You can run it and collect its outputs like this:
```python
outputs = load_iris()
```
And then you can look at the data type of the output using the `type` function, which is built in to Python:
```python
type(outputs)
```
You can also run the function like this to get the different outputs in separate variables:
```python
sepal_length, sepal_width, petal_length, petal_width, y = load_iris()
```
If you have a long list in Python and want to look at just part of it (to get an idea what's inside) you can look at the first ten items like this:
```python
my_long_list[:10]
```

Use the values returned from `load_iris` to answer these questions:
 1. How many flowers are in the dataset?
 2. How many measurements are in the dataset?
 3. What data type is used to represent a collection of measurements (for instance the `sepal_length` variable)?
 4. What numerical data type is used to represent a single measurement? (Remember the `type` function is built in to Python!)
 5. What is in the variable called `y`?

Based on your first initial, you have been assigned a "feature" in this dataset.
"Feature" is a word commonly used in data science to describe a value that is available to make a prediction.
In this case, we will be using features like petal length to predict the species of each iris flower.

| Your first initial | Your assigned feature |
| ------------------ | --------------------- |
| L                  | sepal length          |
| N                  | sepal width           |
| T                  | petal length          |
| B                  | petal width           |

Use Python to calculate the average value of your feature.
Do you remember how we wrote a Python function that calculates the mean of a list of numbers?
Here is a hint at the function we wrote last time.
You need to replace the question marks to make it work.

```python
def mean(list_of_numbers):
    # Step one:
    sum_of_numbers = ???
    for number in list_of_numbers:
        sum_of_numbers = ???
    # Step two:
    number_of_numbers = ???
    # Step three:
    average = ??? / ???
    # Return the average as the output of the function:
    return average
```

Here is a function that computes the standard deviation of a list of numbers, but it needs to be given the mean as an additional argument!

```python
from math import sqrt
def standard_deviation(values, mean):
    accumulator = 0
    for index in range(len(values)):
        value = values[index]
        deviation = value - mean
        deviation_squared = deviation * deviation
        accumulator = accumulator + deviation_squared
    variance = accumulator / len(values)
    std_dev = sqrt(variance)
    return std_dev
```

Use Python to calculate the standard deviation of your feature.

Can you write a Python function that calculates the standard deviation without needing the mean to be provided as an input?
You could write it from scratch, or you could write a function that calls other functions you have already defined, such as `mean` and `standard_deviation`.

Here is a function that takes three inputs and produces one output. The first input, “label”, needs to be a string, and the second argument, “labels”, needs to be a list of strings. The third argument, “values”, needs to be a list the same length as “labels”. 

```python
def select_values_by_label(label, labels, values):
    output = []
    for index in range(len(labels)):
        if labels[index] == label:
            output.append(values[index])
    return output
```

If you want to look at the sepal length of only the iris setosa species, you can call this function:
```python
select_values_by_label("Iris-setosa", y, sepal_length)
```

What are the means and standard deviations of your feature for each species of iris? 
| species    | mean | standard deviation |
| ---------- | ---- | ------------------ |
| setosa     |      |                    |
| versicolor |      |                    |
| virginica  |      |                    |

Is it easier to tell two species apart using your feature when their means are similar or very different?

Is it easier to tell two species apart using your feature when their standard deviations are large or small?

Compare your results to those of another club member.
Can you use mean and standard deviation to make an argument about which features can be used to tell these species apart?
Which species can be identified with these features?

What if there was a way to use more than one feature at a time to distinguish the species?

Are all the species equally easy or difficult to distinguish?
