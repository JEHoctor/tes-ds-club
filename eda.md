# Coding + Statistics = EDA

Here is a function that downloads data about iris flowers from the website of the University of California, Irvine (UCI). Copy this function and run it with load_iris(). What does it do?

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

You can run it and collect its outputs with outputs = load_iris() and then you can look at the data type of the output with type(outputs). You can also get the different outputs in separate variables like this:
sepal_length, sepal_width, petal_length, petal_width, y = load_iris()

How many flowers are in the dataset?
How many measurements are in the dataset?
What data type is used to represent each measurement?
What is in the variable called “y”?

Use Python to calculate the average value of one of these measurements.


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

Use Python to calculate the standard deviation of the measurement whose average you calculated before.

Can you write a Python function that calculates the mean of a list of numbers?
Your Python function to calculate the mean might look like this:

```python
def mean(values):
    # Maybe you need to use a for loop like this?
    for value in values:
        # ... Do something with a single value
    average = # ???
    return average
```

Can you write a Python function that calculates the standard deviation without needing the mean to be provided as an input?


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
select_values_by_label("Iris-setosa", y, sepal_length)

Calculate means and standard deviations for different combinations of species and measurements.

Is it easier to tell two species apart when their means are similar or very different?
Is it easier to tell two species apart when the standard deviations of a measurement within a species are large or small?

Can you use mean and standard deviation to make an argument about which measurements can be used to tell these species apart?
Are all the species equally easy or difficult to distinguish?
