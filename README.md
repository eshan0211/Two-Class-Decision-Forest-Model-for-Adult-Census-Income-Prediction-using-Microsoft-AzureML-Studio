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
