### Introduction
Machine Learning is an area of AI that explores how computers can learn without needing to be explicitly taught. Machine learning can help tackle many real-world problems.

To determine whether cancer cells are `malignant` or `benign,` we must examine their physical properties, which can be used to identify them. A machine learning problem will be addressed using `Scikit-learn`. Scikit-learn, a Python framework, is a free and open-source tool for machine learning, machine mining, and data analysis.

### Prerequisites
1. Using Scikit-learn will be a necessity for our project. 
2. Jupyter notebooks are preferred for this project, however you are free to use any IDE of your choice.
3. Breast cancer wisconsin (diagnostic) dataset will be used in this tutorial therefore ensure its loaded. You can download a copy of UCI ML Breast Cancer Wisconsin (Diagnostic) dataset from [here](https://scikit-learn.org/0.21/modules/generated/sklearn.datasets.load_breast_cancer.html)

### Table of contents
- [Naive Bayes algorithm](#naive-bayes-algorithm)
    - [Advantages of the Naive Bayes classification](#advantages-of-the-Naive-Bayes-classification)
    - [Disadvantages of the Naive Bayes classification](#disadvantages-of-the-Naive-Bayes-classification)
- [The dataset](#the-dataset)
- [Classification implemented with the Scikit-learn framework](#classification-implemented-with-the-scikit-learn-framework)
- [Conclusion](#conclusion)

### Naive Bayes algorithm
Despite its simplicity, Naive Bayes is a potent algorithm for predicting outcomes. In Naive Bayes, each input variable is assumed to be independent, which is why it's named naive. In reality, this is a big assumption, and the technique works well for a wide range of difficult tasks. When assumption of independence holds, a Naive Bayes classifier performs better compare to other models like logistic regression and you need less training data. It perform well in case of categorical input variables compared to numerical variable


This popular method for binary classification, dubbed Naive Bayes, will be selected for use in this model.

### Advantages of the Naive Bayes classification
- It's a snap to put into action.
- Less training data is needed.
- Continuous and discrete data are also supported.
- The number of predictors and data points can be increased indefinitely, making it extremely flexible and adaptable.
- It is rapid and can be used to make predictions in real-time.
- 
### Disadvantages of the Naive Bayes classification
- In naive Bayes, all predictors (or traits) are assumed to be independent, however, this is rarely the case in reality.
- To avoid assigning zero probability to a categorical variable whose category was not accessible in the training dataset, this technique uses the zero-frequency problem. Zero frequency indicates simply a continuous term, no wave, no peaks passing.

### Installations
Run the following line on the command prompt to download and install it on your computer, or [follow this documentation.](https://scikit-learn.org/0.17/install.html)

```bash
pip install scikit-learn
```
> For this project, Jupyter notebook are encouraged, although you are free to use any IDE you choose. Instead of developing an entire script from scratch, one can execute a few lines of code and see what happens one by one rather than writing the entire script and running it.

To set it up, use the command line and enter the following code:

```bash
pip install jupyter
```
### The dataset
We will be classifying cancer cells based on their features and identifying them if they are malignant or benign using scikit-learn library for python programming language. We will be using the [breast cancer Wisconsin dataset](https://scikit-learn.org/0.21/modules/generated/sklearn.datasets.load_breast_cancer.html) for our machine learning problem.

Malignant and benign breast cancer tumors are included in the data set, as well as their respective classification labels. The data set has data of 569 tumors and includes data on 30 attributes of a tumor that we will be using to train our model. The following function can be used to load it:
```python
load_breast_cancer([return_X_y])
```
### Classification implemented with the Scikit-learn framework
#### 1. Adding the required modules and data to the import

Scikit-learn and Breast cancer wisconsin (diagnostic) dataset will be imported into our program as a first step.

```python
import sklearn
from sklearn.datasets import load_breast_cancer
```
#### 2. Creating a variable from the dataset
We must take into account the labels, classification labels, feature meanings, and the data to be learned from this dataset.

```python
data = load_breast_cancer()
```
We've loaded the breast cancer dataset into the data variable.
#### 3. Arranging and analyzing data
Before we can learn how to train our model, we need to organize the data, and if you want to see what it contains, you can use the **print()** function.

```python
# Organizing our data
namesForlabels = data['target_names']
ourlabels = data['target']
namesForfeature = data['feature_names']
ourfeatures = data['data']
```
You can then use the **print()** method to examine the data.

```python
print(namesForlabels)
```
Output:

```bash
['malignant' 'benign']
```
Tumor data is classified as `malignant` or `non-malignant` as you can see.

Labels 0 and 1 are binary values representing labels where 0 indicates malignant tumors and 1 indicates benign tumors when they are written.

```python
print(ourlabels)
```
Output:
```bash
[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 1 0 0 0 0 0 0 0 0 1 0 1 1 1 1 1 0 0 1 0 0 1 1 1 1 0 1 0 0 1 1 1 1 0 1 0 0
 1 0 1 0 0 1 1 1 0 0 1 0 0 0 1 1 1 0 1 1 0 0 1 1 1 0 0 1 1 1 1 0 1 1 0 1 1
 1 1 1 1 1 1 0 0 0 1 0 0 1 1 1 0 0 1 0 1 0 0 1 0 0 1 1 0 1 1 0 1 1 1 1 0 1
 1 1 1 1 1 1 1 1 0 1 1 1 1 0 0 1 0 1 1 0 0 1 1 0 0 1 1 1 1 0 1 1 0 0 0 1 0
 1 0 1 1 1 0 1 1 0 0 1 0 0 0 0 1 0 0 0 1 0 1 0 1 1 0 1 0 0 0 0 1 1 0 0 1 1
 1 0 1 1 1 1 1 0 0 1 1 0 1 1 0 0 1 0 1 1 1 1 0 1 1 1 1 1 0 1 0 0 0 0 0 0 0
 0 0 0 0 0 0 0 1 1 1 1 1 1 0 1 0 1 1 0 1 1 0 1 0 0 1 1 1 1 1 1 1 1 1 1 1 1
 1 0 1 1 0 1 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 1 1 1 0 1 0 1 1 1 1 0 0 0 1 1
 1 1 0 1 0 1 0 1 1 1 0 1 1 1 1 1 1 1 0 0 0 1 1 1 1 1 1 1 1 1 1 1 0 0 1 0 0
 0 1 0 0 1 1 1 1 1 0 1 1 1 1 1 0 1 1 1 0 1 1 0 0 1 1 1 1 1 1 0 1 1 1 1 1 1
 1 0 1 1 1 1 1 0 1 1 0 1 1 1 1 1 1 1 1 1 1 1 1 0 1 0 0 1 0 1 1 1 1 1 0 1 1
 0 1 0 1 1 0 1 0 1 1 1 1 1 1 1 1 0 0 1 1 1 1 1 1 0 1 1 1 1 1 1 1 1 1 1 0 1
 1 1 1 1 1 1 0 1 0 1 1 0 1 1 1 1 1 0 0 1 0 1 0 1 1 1 1 1 0 1 1 0 1 0 1 0 0
 1 1 1 0 1 1 1 1 1 1 1 1 1 1 1 0 1 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
 1 1 1 1 1 1 1 0 0 0 0 0 0 1]
```
The tumor's 30 distinct characteristics and properties may be seen in full detail when the features are printed. Training our model on factors such as a tumor's malignant or benign status will help us make an accurate prediction.

```python
print(ourfeatures)
```
Output:
```bash
[[1.799e+01 1.038e+01 1.228e+02 ... 2.654e-01 4.601e-01 1.189e-01]
 [2.057e+01 1.777e+01 1.329e+02 ... 1.860e-01 2.750e-01 8.902e-02]
 [1.969e+01 2.125e+01 1.300e+02 ... 2.430e-01 3.613e-01 8.758e-02]
 ...
 [1.660e+01 2.808e+01 1.083e+02 ... 1.418e-01 2.218e-01 7.820e-02]
 [2.060e+01 2.933e+01 1.401e+02 ... 2.650e-01 4.087e-01 1.240e-01]
 [7.760e+00 2.454e+01 4.792e+01 ... 0.000e+00 2.871e-01 7.039e-02]]
```
There are 569 instances of tumor data in the dataset in question, each with a numerical value for one of the 30 variables in question. 

So, from the above data, we can conclude that the first instance of tumor is **malignant** and it has a mean radius of value 1.79900000e+01. 
#### 4. Creating sets of data to organize the information
We need to evaluate our classifier's accuracy by running it on data that has never been seen before.This means we'll divide our data into two sets, the training and test sets, before we begin creating our model. Training and evaluation of the model will be done on the training set, and then it will be used to predict the unknown test set.

Sklearn comes with a function called **train test split()**, which automatically divides the data into these two groups for us.

```python 
from sklearn.model_selection import train_test_split

train, test, trainingLabels, testingLabels = train_test_split(ourfeatures, ourlabels, test_size = 0.33, random_state = 42)
```
It is possible to utilize the test size as a parameter to randomly divide the data. We've divided the original data into test data by a third of its original size. Other than that, the rest of the data is used for training. A different label for the train and test variables is used for each.

Refer to the [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html) for further information on how to use **train_test_split**() function.

#### 5. Building the Model
You can select from a wide variety of machine learning models to meet your needs. Each one has advantages and cons of its own. A popular method for binary classification, dubbed `Naive Bayes,` has been selected for use in this model. GaussianNB is the first module that needs to be imported and initialized using **GaussianNB()** function and then use the **fit()** method to train your model on the dataset's data.

```python
from sklearn.naive_bayes import GaussianNB

gaussiannb = GaussianNB()
ourModel = gaussiannb.fit(train, trainingLabels)
```
To generate predictions on our test set, we first need to finish training the model. The built-in **predict()** function returns a prediction value array for each data point in the test set. Our forecasts will be displayed using the **print()** method.

```python
ourPredictions = gaussiannb.predict(test)
print(ourPredictions)
```
Output:
```bash
[1 0 0 1 1 0 0 0 1 1 1 0 1 0 1 0 1 1 1 0 1 1 0 1 1 1 1 1 1 0 1 1 1 1 1 1 0
 1 0 1 1 0 1 1 1 1 1 1 1 1 0 0 1 1 1 1 1 0 0 1 1 0 0 1 1 1 0 0 1 1 0 0 1 0
 1 1 1 1 1 1 0 1 1 0 0 0 0 0 1 1 1 1 1 1 1 1 0 0 1 0 0 1 0 0 1 1 1 0 1 1 0
 1 1 0 0 0 1 1 1 0 0 1 1 0 1 0 0 1 1 0 0 0 1 1 1 0 1 1 0 0 1 0 1 1 0 1 0 0
 1 1 1 1 1 1 1 0 0 1 1 1 1 1 1 1 1 1 1 1 1 0 0 1 1 0 1 1 0 1 1 1 1 1 1 0 0
 0 1 1]
```
#### 6. Accuracy testing of the model trained
If we want to make sure our model is accurate, we may compare the predictions it makes to the actual labels in the testing set. Use the sklearn module built-in **accuracy_score()** function for this task.

```python
from sklearn.metrics import accuracy_score

print(accuracy_score(testingLabels, ourPredictions))
```
Output:

```bash
0.9414893617021277
```
If a tumor is malignant or benign, our studies show that this machine learning classifier based on the `Naive Bayes` algorithm is 94.15% accurate.

To see the whole code for this tutorial, click [here](https://colab.research.google.com/drive/1Ztr7e9qZ9nrLHSGXJ1EAjBplNGXXtjC7?usp=sharing).

### Conclusion
Determination can be done by looking at the features of cancer cells, which can indicate whether they are `malignant` or `benign.` We used `scikit-learn` to address a machine learning problem. Python framework Scikit-learn is a free and open-source tool for machine learning, machine mining, and data analysis.

---
Peer Review Contributions by: [Willies Ogola](/engineering-education/authors/willies-ogola/)