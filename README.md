# honors_contract_BMI110

# Project Explanation
In this project, we have a csv file with multiple columns. The column with the name ```stroke``` contains dependent values in form of ```0``` and ```1```, where 1 means ```Yes``` and 0 means ```No```. The rest of the columns have independent values which influcence the dependent variable.


My task was to train a model, which, when provided specific values from the user, would be able to provide us with information about whether a person has a chance of having a stroke or not. The steps for this were:

    1) Data Preprocessing: Encoding categorical values, dropping the 'id' column, and filling the missing values in the 'bmi' column.
    2) Making the model and training it.
    3) Testing the model and providing its percentage accuracy along with a confusion matrix.
    4) Visualizing the results in form of a heatmap.
    5) Providing an example of what getting predictions from custom data would look like.


# Explanation of the steps

### Data Preprocessing


First we import the libraries that are required. We will use ```os``` to determine the path of the file, ```numpy``` and ```pandas``` to manipulate data, ```matplotlib``` to visualize data, ```sklearn``` to make model and train it and 'imblearn' to prevent overfitting of the data.
We then load the csv file, read it using the ```pandas``` library and store it in a variable called ```dataset``` which is of the form of a dataframe. Then we drop the ```id``` column since we know that it does not affect the chance of a person having a stroke or not. We fill the missing values in the column with index 8. ```fillna``` is an inbuilt function of the pandas library that we used to fill in the missing values with the mean of the rest provided values of bmi. We then split the dataframe into dependent variables and independent variables. ```x``` represents the independent variable and ```y``` represents the dependent variable. We do this using the ```iloc``` function provided by pandas as well. We now need to encode the categorical data in the dataset into numbers, which is readily understood by a model. We use the ColumnTransformer and OneHotEncoder class together to achieve this. We create an obejct of the class ColumnTransformer and name it ```transformer```. We then provide two parameters to the class named ```transformers``` and ```remainder```. We provide a tuple inside of a list containing information about what encoder we want to use, and what column we need to encode. We then pass this information to a parameter named ```transformers```. As for the ```remainder``` parameter, we can either pass ```passthrough``` or ```drop``` to it. ```passthrough``` in this case ignores the rest of the colums which we did not provide to it and ```drop``` would delete or drop the rest of the columns which we did not provide. We then proceed to transform the data. The next step would be to resample the data. From the dataset you would be able to tell that the number of ```0``` values is significantly more than the number of ```1``` values in the stroke column. This would lead to the model becoming very good at predicting 0 and very poor at predicting 1. This would provide a false accuracy and our model would not be considered good and useable. We somehow need a way for the model to predict both values accurately. We therefore use the ```imblearn``` library for this. imblearn stands for imbalanced learn. We create an object called ros and use the ```fit_resample``` function of that class to achieve our balance of data and store our new data in ```x_resampled``` and ```y_resampled```. The next step would be to split the data into training set and testing set, so that we can train the model using a specific proportion of the data and use the rest to test the data. We use sklearn's train_test_split function to do this and store the train variables and test variables of both the independent and dependent variables inside ```x_train```, ```x_test```, ```y_train```, ```y_test```. We provide the ```test_size``` of 0.3 meaning that the training data will constitude 70% of the original data and the test data will be 30% of the original data. ```random_state``` parameter just states the arrangement of randomized data.  


### Model building and training



We now proceed to create the model and train it. I chose the RandomForestClassifier because it provided the most accuracy. There are several other models we can use for classification, but the choice of model would depend on what kind of data you are using and what model would provide the best accuracy for that particular type of data. I made an object called 'classifier' of the class 'RandomForestClassifier' which is essentially our model and we provide it some parameters called 'n_estimators', which stands for the number of decision trees we will be using, 'criterion', and 'random_state' which essentially stands for the way in which the data is ararnged randomly. You can think of it as a 'seed'. We train the model on ```x_train``` and ```y_train``` values using the 'fit' function provided by our class. 


### Model testing



We make the model predict the values of ```x_test``` and store the predictions in a variable called ```y_pred```. To determine the accuracy we will somehow need a way to tally ```y_pred``` and ```y_test```. We use sklearn's 'accuracy_score' to do this, and we also use sklearn's 'confusion_matrix' to provide more details about the accuracy. We make the confusion matrix by providing ```y_test``` and ```y_pred``` as the parameters and then print the confusion matrix and accuracy_score as well. Reading the confusion matrix is quite easy, but tricky to figure out at first. The general rule of thumb is that the diagonal values from the top left to the bottom right of the confusion matrix should be the greater as compared to the other values, and significantly greater than the other diagonal as well.


### Visualizing the data


We use matplotlib's pyplot function to plot a heatmap for the confusion matrix. We use ```plt.imshow``` to generate a heatmap by passing the confusion matrix and the color we need the heatmap to be as the parameters. ```plt.colorbar``` just provides a colorbar to the right and ```plt.show``` is just a way to conclude the graph or the heatmap, to update the heatmap for every value of x or y being changed and to actually show the graph in a interactive window. 


# Entering your own data


We now can enter our own data and make the already trained model to predict what the chance of a person having a stroke can be. However, the tricky part will be to provide our data to the model since the model expects us to provide data in a transformed way and of the same dimensions as provided before. So we will need to preprocess the data again. 


We first enter our data in form of a list and use ```np.array(list).reshape(1, -1)``` to make the data in form of a row and not a column and also transform it into a 2d array, which the model expects. We then transform the data, or encode the categorical values of the data using the same transformer we used earlier. It is imperative to use the transformer we created earlier since it had already been fitted to the x values we provided earlier and now has the information to transform the data we provided it into the same form that it converted or transformed the x values into. We then use the 'classifier.predict' function to predict the results and store it in a variable. Now the final step will be to print out the result in human readable form, since we will get the output in form of either 1 inside of a list or 0 inside of a list. This is quite easy and we can do this using conditionals and if statements. We can say that if the first element of the output is 1 then print out that you do have a chance of having a stroke or else print out that you do not have a chance of having a stroke. Note that we will either get the results in form of a 0 or 1 only since this is a classification problem, so it is okay to use else. 


