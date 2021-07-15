# Two Class Decision Forest for Adult Census Income Prediction using Microsoft AzureML Studio

- The problem at hand is to predict whether a particular person earns more than 50,000 per year or not. We are going to use one of the sample datasets named adult census dataset.
- Sign in to your Microsoft azure account. ( you can make a free trial account for a month [here](https://azure.microsoft.com/en-in/free/search/?&ef_id=CjwKCAjwlrqHBhByEiwAnLmYUA_xQpYpL-GyL0_xeq6PiMMIEJoCUSsH0t9AEomzarx65DD4luwkcBoCEUoQAvD_BwE:G:s&OCID=AID2200195_SEM_CjwKCAjwlrqHBhByEiwAnLmYUA_xQpYpL-GyL0_xeq6PiMMIEJoCUSsH0t9AEomzarx65DD4luwkcBoCEUoQAvD_BwE:G:s&gclid=CjwKCAjwlrqHBhByEiwAnLmYUA_xQpYpL-GyL0_xeq6PiMMIEJoCUSsH0t9AEomzarx65DD4luwkcBoCEUoQAvD_BwE) but will also have to add your credit card details)
- We will use the [Microsoft Azure Machine learning studio](https://studio.azureml.net) which is great for beginners.

## 1)Visualising the dataset : 
   - Drag and drop the dataset `Adult Census Income Binary Classification dataset` (available in the sample datasets) in the working space and visualise it : 
   - <img width="1115" alt="Screen Shot 2021-07-16 at 3 20 55 AM" src="https://user-images.githubusercontent.com/55271617/125862455-2fd588c8-6c26-4d12-95f6-df0fa60f048a.png">
   - <img width="1110" alt="Screen Shot 2021-07-16 at 3 22 41 AM" src="https://user-images.githubusercontent.com/55271617/125862631-5c443b41-a50b-4fdb-8021-f00d90a75c92.png">
   - It has more than 32,000 records and 15 columns or features.
   - Try to vusialise every column, for eg `Workclass` is type of employment such as private, self-employed, state or local government or federal
government, without pay and so on. It has got 8 unique values and 1,836 missing values.
   - Fnlwgt is nothing but the number of people the census takers believe that observation represents. That may not have any significant impact and we are going to assume that these records are of individual and hence will ignore this column.
   - Visualise rest of the columns in the same way.
   - At last, the column `income` represents the value of whether or not the person makes more than $50,000 per annum. It has only two categorical values, more than 50,000 and less than or equal to 50,000.
   - Now we will replace the missing values from our dataset. (You might have has noticed that missing values are only in the string type of features)

## 2)Replacing the Missing Values :
   We should clean this missing data so that our model can work on neat and clean information.
   - Drag and drop the `Clean Missing Data` Module in your workspace.
   - Connect the adult census data to this module and let's select the columns that have missing values. So let's launch the column selector.
   - We have missing values in workclass, occupation and native country.
   - <img width="1110" alt="Screen Shot 2021-07-16 at 3 42 53 AM" src="https://user-images.githubusercontent.com/55271617/125864496-33026c5f-f98f-49a8-b403-f42c469c1e88.png">
   - We want to replace these values with the most frequent value in the respective column. Hence, we select replace with mode. 
   - We have kept values of `Minimum missing value ratio` and `Maximum missing value ratio` as 0 and 1 respectively cause we want to replace all the missing values.
   - Now you can run the module and visualise the data. (no missing values)
   
   ## 3)Selecting Features (Columns) :
- Couple of columns such as `fnlwgt` and `education-num`, are of no use for us. So, we are going to drop them from the experiment and select only the remaining ones.
- Drag and drop the `select columns in dataset` module in your workspace.
- <img width="1110" alt="Screen Shot 2021-07-16 at 3 48 42 AM" src="https://user-images.githubusercontent.com/55271617/125864952-4c5d86e3-d05a-4fd4-8595-c03b1bd82ae6.png">

## 4)Making our data categorical :
- All of the non-numeric columns of this dataset are string. However, all of them represent only categorical values and should be changed to the same.So let's get the `edit metadata` module and change the variables to categorical type. (for columns, refer the photo given below)
- <img width="1110" alt="Screen Shot 2021-07-16 at 3 53 04 AM" src="https://user-images.githubusercontent.com/55271617/125865359-8fd4882c-010b-4c7f-8db0-6a83c4d5fb60.png">


## 4)Splitting Data :
We will split the existing data and use part of the data for training our model and the rest for testing the result as well as validating the results for accuracy.
- Drag and drop the `split data` module.
- We will split the data in 70:30 ratio and lets do the [stratified split](https://stats.stackexchange.com/questions/250273/benefits-of-stratified-vs-random-sampling-for-generating-training-data-in-classi) on the column, `income` so that we have even distribution of values between train and test dataset.
- Now Run the `split data` module and visulaise the two output nodes.(one has 70 percent data and one 30 percent)
- <img width="1110" alt="Screen Shot 2021-07-16 at 3 57 15 AM" src="https://user-images.githubusercontent.com/55271617/125865746-8da83513-01a9-422f-a04c-b079e3c2552e.png">

## 5)Training and scoring our two-class Logistic Regression Model :
We are going to predict an outcome that's either yes or no, which means that we are only predicting two classes, so we will use two-class Decision Forest module.
- Drag and drop the `Two- Class Decision Forest` Module, you can also change the parameters and visualise the change in results with different values of parameters.
- <img width="600" alt="Screen Shot 2021-07-15 at 8 54 34 PM" src="https://user-images.githubusercontent.com/55271617/125814268-b98b7ed6-1f8f-4026-9c71-9eb26dca1939.png">
- Lets set the parameters now (we can always use the default set as well):
    - Resampling Methods (Bagging and replicate) : 
      - In bagging method, each tree is grown on a new sample. Created by randomly sampling the original dataset with replacement until you have a dataset as the size of the original. And the output of the modules are combined by voting which is a form of aggregation.
      - In case of replicate, each tree is trained on exactly the same input data. The determination of which split predicate is used for each tree node remains random and the trees will be of diverse nature.
    - Number of Decision Trees we want to build.
    - Maximum depth of the Decision Tree : It is nothing but how many levels below the root. Increasing the depth of the tree might increase the precision but at the risk of some overfitting and increased training time.
    -Number of random splits per node : It is nothing but number of splits we want when building each node of the tree. A split here, means that features in each level of the tree are randomly divided.
    
- For training our model, drag and drop the `train model` module (selecting income as the column selector) and connect them as shown below.
- <img width="1110" alt="Screen Shot 2021-07-16 at 4 14 57 AM" src="https://user-images.githubusercontent.com/55271617/125867182-37942b10-b495-4db0-aaba-5675e8893ea7.png">

- The model is ready to be trained, we want to score the algorithm on our test dataset and see how it performs. So the module that is required for the same is called as a score model, which is basically a validation module for our trained algorithm. So let's search for it and drag and drop it hereand as you will see, it requires 2 inputs. The first one is the train model which is nothing but the output from the train model module and the test dataset.
- So we provide the connection of our train model as well as the test dataset. The test dataset is coming from the second node of split module. Now, let's right click on it and run selected. It will run all the previous steps that have not been executed so far.
- <img width="1110" alt="Screen Shot 2021-07-16 at 4 20 15 AM" src="https://user-images.githubusercontent.com/55271617/125867552-c4ef49a7-8403-4b98-9904-aeaa046e29dc.png">
- Now we can visualise the output.
- <img width="1110" alt="Screen Shot 2021-07-16 at 4 20 49 AM" src="https://user-images.githubusercontent.com/55271617/125867590-cd8af53b-bb52-49dc-9442-e8e76e8da530.png">
- As you can see, there are two additional columns called scored label and score probabilities, scored label is the predicted value of that particular set of features or rows and score probability is the probability with which this particular value has been predicted.

## 6)Evaluating our model :
Lets visualize these results in a bit more structured manner.
- We will use a module called `evaluate model` for evaluating our results.
- It takes 2 nodes which are for evaluating different models. The second one is optional and let's connect our scored model to the first node and run it.
- <img width="1110" alt="Screen Shot 2021-07-16 at 4 22 34 AM" src="https://user-images.githubusercontent.com/55271617/125867758-4d19928e-e635-4ad0-b29f-44428e15f6b7.png">
- After visulising the output, we can say the accuracy is around `85%` and the AUC i.e area under thecurve is also very high which means that the model is a very good model.
- <img width="1242" alt="Screen Shot 2021-07-16 at 4 24 45 AM" src="https://user-images.githubusercontent.com/55271617/125867893-34c1397b-dd6c-42cc-86fb-630f393a0adc.png">

We were able to successfully predict the income level for a particular observation with very high accuracy.

## Thank You, Hope the explanation was clear and to the point !
