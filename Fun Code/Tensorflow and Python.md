# Learning Tensorflow and Python

### Introduction

Tensorflow is enormous and memorization of the syntax is difficult. Familiarity with documentation and techniques is essential to learning.

The below algorithms are common applications.

###### Tensorflow Algorithms

* Linear Regression
* Classification
* Clustering
* Hidden Markov Models

### Linear Regression In Tensorflow



###### Implementation in Tensorflow

I am going to use gradient descent because that is more generally applicable to ML tasks.



### Classification In Tensorflow

Similar to a linear regression, uses the properties of data to classify the type of the input. Difference is that its categorical rather than numeric.

###### Worked Example is Using the Titanic Dataset

For each column, higher/lower value corresponds to a higher chance of survival. 

Training Data: https://storage.googleapis.com/tf-datasets/titanic/train.csv

Testing Data: https://storage.googleapis.com/tf-datasets/titanic/eval.csv

Need to distinguish between **categorical** and **numeric** data. Categorical data needs to be transformed to numeric. Ex: male and female ~> 0 and 1

```python
# Defines the features that we will be utilizing formally in feature_columns array.
CATEGORICAL_COLUMNS = ['sex', 'n_siblings_spouses', 'parch', 'class', 'deck', 'embark_town', 'alone']
NUMERIC_COLUMNS = ['age', 'fare']

feature_columns = [] #Build up an array of 'feature columns'
for feature_name in CATEGORICAL_COLUMNS:
    vocabulary = dftrain[feature_name].unique() #Array of uniques
    feature_columns.append(tf.feature_column.categorical_column_with_vocabulary_list(feature_name, vocabulary))
    
for feature_name in NUMERIC_COLUMNS:
    feature_columns.append(tf.feature_column.numeric_column(feature_name, dtype=tf.float32))
```

Creates tensorflow columns that specify the type of data that will be passed to the linear regression algorithm.



###### Training Process

Data is fed into the model in **batches** and in **epochs**. Batches are the number of rows fed into the training function at a time (lazy-loading large datasets). Epochs are the number of times the model will see the same data (useful when small training dataset).

The data is feed into the algorithm in batches and epochs. How this is done is handled by the **input function**.

###### Input Function

The tensorflow model requires data to be passed in as a 'tf.data.Dataset' object. The input function will take the pandas dataframe and convert it to that object.

Comes straight from tensorflow documentation.

```python
def make_input_fn(data_df, label_df, num_epochs=10, shuffle=True, batch_size=32):
    def input_function(): #inner function is returned
        ds = tf.data.Dataset.from_tensor_slices((dict(data_df), label_df)) #create Dataset object with data and labels
        if shuffle:
            ds = ds.shuffle(1000) #Shuffles data.
        ds = ds.batch(batch_size).repeat(num_epochs) #Split dataset into batches of 32 repeating for each epoch
        return ds #Return a batch of the dataset
    return input_function #Return a function object for use.

#For our regression:
#Input the data and label df's
train_input_fn = make_input_fn(dftrain, y_train) 

#Also make input function for testing data
eval_input_fn = make_input_fn(dfeval, y_eval, num_epochs=1, shuffle=False)
```

###### Creating, Training, and Testing the Linear Classifier Model

```python
linear_est = tf.estimator.LinearClassifier(feature_columns=feature_columns)
linear_est.train(train_input_fn) #Trains the model
result = linear_est.evaluate(eval_input_fn) #Tests the testing data based on trained model
clear_output()
print(result['accuracy'])
```

###### Using the Trained and Tested Model

Each prediction made by the model is a dictionary containing probability of outcome among other things

```python
result = list(linear_est.predict(eval_input_fn)) #to use the model need to pass it another input_function()

print(dfeval.loc[3]) #Prints the passenger's info
#Each prediction made by the model is a dictionary. Index for probs to get survival probability.
print(result[3]['probabilities'][1])

```

# **h1** hello

## **h2** hello

### **H3** hello

#### **H4** hello

##### **H5** hello

###### **H6** hello

>#### hello
>
>##### hello
>
>###### hello





