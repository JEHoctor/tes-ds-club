# NASA Landsat Satellite Data Science

Rember to install the ucimlrepo package in your Colab notebook.

```
!pip install ucimlrepo
```

We're going to work with the [Statlog dataset](https://archive.ics.uci.edu/dataset/146/statlog+landsat+satellite) today.

```python
from ucimlrepo import fetch_ucirepo

# fetch dataset 
statlog_landsat_satellite = fetch_ucirepo(id=146)

# data (as pandas dataframes)
X = statlog_landsat_satellite.data.features
y = statlog_landsat_satellite.data.targets
```

The variable `X` (be careful, it's capital X) is a "DataFrame," which is a table of data with rows and columns.
It is more flexible and powerful than the lists we have used so far.
`X` contains numerical readings from a satellite imaging system.

```python
type(X)
```

`X` has 6435 rows and 36 columns.
Each row is a different location on the ground that has been imaged by the satellite, and each column is a different type of measurement made by the satellite.

```python
X.shape
```

Here's how easy it can be to get information from a DataFrame:

```python
# Tells us what the columns are called. This dataset doesn't
# have very useful column names, but that's not always true.
X.columns
```

Also, look how easy it is to get means and standard deviations:

```python
X[["Attribute1", "Attribute2", "Attribute3", "Attribute4", "Attribute5"]].describe()
```

The variable `y` (lowercase) has 6435 rows, but only one column.
It contains the values we want to predict, which are types of soil at the location imaged by the satellite.

```python
y.shape
```

This code plots the first two attributes of the data. The data is color coded by the soil type that we are trying to predict.

```python
import seaborn as sns
sns.scatterplot(data=X, x="Attribute1", y="Attribute2", hue=y["class"], palette="Set1");
```

Notice how the different soil categories overlap. Maybe we could try different attributes? No matter what we try, we will not be able to tell the soil types apart on a plot like this.

We're going to use a model called k-nearest neighbors (k-NN) to make predictions.
Before we train k-NN, we need to split up the data so that we can measure how well the k-NN can make predictions.
We will use the training data to train the k-NN and the testing data to measure how well it can do.

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, stratify=y, random_state=42)
```

Notice the part that says `test_size=0.33`. That means that one third of the data will be used for testing, and won't be in the training data.
The part that says `stratify=y` tells the `train_test_split` split function to make sure that the proportion of soil types is the same in the train and test data as it is in the whole dataset.

Now we will train the k-nearest neighbors model on the training data.

```python
from sklearn.neighbors import KNeighborsClassifier
neigh = KNeighborsClassifier(n_neighbors=3)
neigh.fit(X_train, y_train["class"])
```

We need to make predictions on the testing data using the k-NN model.

```python
y_predictions = neigh.predict(X_test)
y_predictions
```

How well did we do? What do the values in the classification report mean?
What are precision, recall, accuracy, and f1-score?

```python
from sklearn.metrics import classification_report
print(classification_report(y_test, y_predictions))
```

This code plots a Receiver Operating Characteristic curve, which compares our k-NN model to random chance.

```python
from sklearn.metrics import RocCurveDisplay
predicted_probability_y_is_four = neigh.predict_proba(X_test)[:, 3]
is_y_actually_four = (y_test == 4)
rcd = RocCurveDisplay.from_predictions(
    y_true=is_y_actually_four,
    y_pred=predicted_probability_y_is_four,
    plot_chance_level=True,
    name="k-NN",
)
rcd.ax_.set_xlabel("False Positive Rate (Positive label: 4)")
rcd.ax_.set_ylabel("True Positive Rate (Positive label: 4)");
```

Can we do better if we use one these other classification techniques from scikit-learn?
 1. [MLPClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html)
 2. [DecisionTreeClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)
 3. [GaussianNB](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.GaussianNB.html)
