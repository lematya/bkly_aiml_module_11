# bkly_aiml_module_11
Prem's Berkeley AI/ML submission for Module 11
BUSINESS UNDERSTANDING
The task is to use a dataset containing attributes of used cars and their prices to create a model to predict the price attributed given these attributes which include descriptions of the car's structure and features as well as its age, mileage, and condition at time of sale. The aim is to find those attributes whose values strongly influence the price of the car.

DATA UNDERSTANDING
The data consists of a very large number of rows, in excess of 400k rows, but many columns had missing values.
A visual exploration of the Price column, (the target column to be predicted) showed the presence of outliers which were either priced very low, below $1000, or very high, above $200k, with some prices above $1 billion. The vintage of the cars ranged across the 20th century all the way to 2022. Due to the extremely large  price values, a histogram of was of no help as it compressed most of the values into something you could not see. It was more instructive to visualize the distribution of the logarithm of the Price.  Once outliers mentioned above were removed, the log10(price)  approximated a normal distribution centered around a value of 4 (i.e. a price of $10k), and it seemed reasonable to  investigate its relationship to other features such as Year, Odometer, Size, Drive, Fuel Type, etc. 

It turned out there was a discernible negative trend in log10(price) plotted against Odometer, confirming the basic intuition that cars with more mileage would be sold at lower prices. Likewise, a nearly linear positive relationshp existed between the median log10(price) and the Year of the vehicle's manufacture, also confirming intuition that newer cars would fetch higher prices. Furthermore, relationships of the median log10(price) with each of the categorical variables Condition, Size, and Drive appeared to match intuition although not perfectly

For the above reasons, it seems reasonable to begin by investigate various models using some combination of   Year, Odometer, Condtion, Size, and Drive and to use logprice (i.e. log10(price)) as the Target instead of Price, with the understanding that if the errors were very high, a different set of attributes would be considered.

DATA PREPARATION
The Dataset was purged of all rows missing data in any of the chosen input features
For the Numeric features Year and Odometer, a StandardScaler was applied, and polynomial features of upto degree 2 were created
For the Categorical features (Condition, Size, and Drive), features were created using One-Hot Encoding
The Training and Test sets were created using 80% of the dataset for training and 20% for testing.

MODELING
A Ridge model was used along with a GridSearch to apply regularization and search for the best value of the hyperparameter alpha

EVALUATION
The results showed a best alpha value of 0.1 and  the best CV Score (Negative Mean Squared Error) of -0.043529346739052566
The MSE on the test set was 0.0448

The coefficients of the various features for the best model are:
  year: 0.1791695335800416
  odometer: -0.0752801951553068
  year^2: 0.02861026193091628
  year odometer: 0.025495166359333323
  odometer^2: 0.0052798330782782045
  condition_excellent: 0.12227906700198074
  condition_fair: -0.185428593050058
  condition_good: 0.07335395575277127
  condition_like new: 0.10637852027821428
  condition_new: 0.1211236678658358
  condition_salvage: -0.2377066185014872
  size_compact: -0.03361973333173847
  size_full-size: 0.08539575403491363
  size_mid-size: -0.015450833161994009
  size_sub-compact: -0.036325187582753236
  drive_4wd: 0.09272926686387602
  drive_fwd: -0.16947726366190852
  drive_rwd: 0.07674799677635033

