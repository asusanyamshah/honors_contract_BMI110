# honors_contract_BMI110

# Project Explanation
In this project, we have a csv file with multiple columns. The column with the name stroke contains dependent values in form of 0 and 1, whereby 1 meaning 'Yes' and 0 meaning 'No'. The rest of the columns have independent values in them which influcence the dependent value.


My job was to train a model, which, when provided specific values from the user can provide us information about whether a person has a chance of having a stroke or not. The steps included were:

    1) Data Preprocessing: Encoding categorical values, dropping the id column, and filling the missing values
    2) Making the model and training it
    3) Testing the model and providing its percentage accuracy along with a confusion matrix
    4) Visualizing the results in form of a heatmap
    5) Providing an example of what trying to input personalized data would look like


# Explanation of the steps

### Data Proprocessing


First we import the libraries that are required. We will use os to determine the path of the file, numpy and pandas to manipulate data, matplotlib to visualize data, sklearn to make models and train the data and imblearn to reduce overfitting of the data.
We then load the csv file, read it using the pandas library and store it in a variable called 'dataset' in form of a dataframe. Then we drop the 'id' column since we know that it does not affect the chance of a person having a stroke or not. We fill the missing values in the column with index 8 after the index column has been removed. fillna is an inbuilt function of the pandas library that we used. We then split the dataframe stored in a variable named 'dataset' into dependent variable, y and independent variables, x. We do this using the iloc function provided by pandas as well. We now need to encode the categorical data in the dataset into numbers, a form readily understood by a model or a computer. We use the ColumnTransformer and OneHotEncoder class in synchony to achieve this. We create an instance of a class ColumnTransformer and name it 'transformer'. We then provide two parameters to the class named 'transformers' and 'remainder'. We provide a tuple inside of a list containing information about what encoder we want to use, and to what column do we need to apply this, we then pass this information as a parameter 'transformers'. As for the remainder parameter, we can either pass 'passthrough' or 'drop' to it. 'passthrough' in this case means ignore the rest of the colums which i did not provide and 'drop' would mean to delete or drop the rest of the columns which i did not provide. We then proceed to transform the data. The next step would be to resample the data. From the dataset you would be able to tell that the number of '0' values is significantly more than the number of '1' values in the stroke column. This would lead to the model becoming very good at predicting 0 and very poor at predicting 1. This would provide a false accuracy and our model would not be considered good and useable. We somehow need a way for the model to predict both values accurately. We therefore use the 'imblearn' library for this. imblearn intuitively stands for imbalanced learn. We create an object called resampler and use the 'fit_resample' function of that class to achieve our balance of data and store our new variables in x_resampled and y_resampled. The next step would be to split the data into training set and testing set, so that we can train the model using a specific proportion of the data and use the rest to test the data. We use sklearn's train_test_split function to do this and store the train variables and test variables of both the independent and dependent variables inside x_train, x_test, y_train, y_test. We provide the test_size of 0.3 meaning that the training data will constitude 70% of the original data and the test data will be 30% of the original data. 'random_state' parameter just states the arrangement of randomized data.  


### Model building and training



We now proceed to create the model and train it. I chose the RandomForestClassifier because it provided the most accuracy. There are several other models we can use for classification, but the choice of model would depend on what kind of data you are using and what model would provide the best accuracy for that particular type of data. I make an object called 'classifier' which is essentially our model and we provide it some parameters called 'n_estimators', which stands for the number of decision trees we will be using, 'criterion', and 'random_state' which essentially stands for the way in which the data is ararnged randomly. You can think of it as a 'seed'. We train the model on x_train and y_train values using the 'fit' function provided by our class. 


### Model testing



We make the model predict the values of x_test and store the predictions in a variable called y_pred. To determine the accuracy we will somehow need a way to tally y_pred and y_test. We use sklearn's accuracy_score to do this, and we also use sklearn's confusion matrix to provide more details about the accuracy. We make the confusion matrix by providing y_test and y_pred as the parameters and then print the confusion matrix and accuracy_score as well. Reading the confusion matrix is quite easy, but tricky to figure out first. The general rule of thumb is that the diagonal values from the top left to the bottom right of the confusion matrix should be the maximum compared to other values, and significantly greater than the other diagonal as well.


### Visualizing the data


We use matplotlib's pyplot function to plot a heatmap for the confusion matrix. We use plt.imshow to generate a heatmap by passing the confusion matrix and the color we need the heatmap to be as the arguments. plt.colorbar just provides a colorbar to the right and plt.show is just a way to conclude the graph or the heatmap, to update the heatmap for every value of x or y being changed and to actually show the graph in a interactive window. 



