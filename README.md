# Credit_Score_Classification
## Source
The dataset was provided by out instructor, the original source is believed to be the Credit Score Classification dataset by Rohan Paris from Kaggle. There was 2 dataset: 
- Train.csv: the dataset contains 27 Independent Variables and 1 Dependent Variable (i.e Credit_Score).
- Test.csv: the dataset contains 27 Independent Variables and no Dependent Variable (i.eCredit_Score). So, we need to find it for this dataset.

## Machine Learning Models Used
After completing preprocessing, the train.csv dataset was used to train the following models:
  Logistic Regression
  Random Forest Classifier
  XGBoost Classifier
  LightGBM Classifier

The best-performing model was then applied to the test.csv to predict Credit_Score.

## Datatypes of Train.csv and Test.csv
The dataset includes mixed data types, typical of real-world financial data:
- int64: For values like Age, Number_of_Bank_Accounts, etc.
- float64: For continuous values like Monthly_Inhand_Salary, Total_EMI_per_Month
- object: For categorical/text data like Occupation, Payment_Behaviour, Credit_Mix
These required appropriate transformations before feeding into ML models.

## Problems Encountered
After checking the details of dataset by .head(), .info() and .dtypes, it is found that it had: 
- Unnecessary columns
- Columns have mixed types
- Comma separated value in one cell  NaN values
- Outliers

## Preprocessing Steps
So, following steps were performed for the data cleaning and preprocessing:
- Dropping unnecessary columns:
Unnecessary identifiers such as ID, Customer_ID, Name, and SSN were dropped from the dataset as they do not contribute to the prediction of credit scores. 

-  Transforming correct datatypes:
Several important columns like Age, Annual_Income, Num_of_Loan, and others converted from object to numeric values, with any conversion errors replaced by NaN for safe handling. Additionally, month names were mapped to numeric positions, and Credit_History_Age was transformed from text (22 Years and 1 Months) to numeric format (265).

- Checking the object values:
While inspecting object-type columns, unusual placeholder values like '________', '_', and '!@9#%8' were found in Occupation, Credit_Mix, and Payment_Behaviour. Such values were treated as missing (NaN) and handled appropriately during preprocessing.

- Encoding the object datatypes:
  Label encoding:-
Label encoding was performed using LabelEncoder from sklearn on standard categorical columns, ensuring consistent numerical representation. For columns with custom value logic, manual mapping was applied to assign meaningful numeric codes. This helped standardize non-numeric values like "Yes", "No", or "NM" into machine-readable formats.
  MultiLabel Binarizer Encoding:-
The Type_of_Loan column contained multiple loan types in a single cell, separated by commas. To handle this, MultiLabelBinarizer was used to split these entries and convert them into multiple binary columns. This allowed the model to recognize the presence or absence of
each loan type individually.

- Checked duplicates:
To check for duplicate records in the dataset, .duplicated().sum() was used. The result returned np.int64(0), indicating that the dataset contains no duplicate rows. Hence, no further action was required for duplicate handling.

- Checked and replaced null values:
Upon checking for null values, several numeric columns like Age, Annual_Income, Monthly_Inhand_Salary, and others were found to contain missing entries. To handle this, NaN values were replaced using the median of each respective column.

- Checked Outliers and replaced with medians:
Outliers were checked in numeric columns using visual tools like boxplots and value counts. Suspicious values with low shrink or large spikes were found and replaced with the median of the respective column. This approach preserved data integrity while minimizing the impact of extreme values.

## Conclusion
Based on the combination of evaluation metrics like accuracy, precision, recall, F1-score, and confusion metrices observations, the Random Forest is the best model of the classification of credit score.
