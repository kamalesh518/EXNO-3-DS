EXNO-3-DS
NAME : kamalesh y
REG NO : 24004024
AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

ALGORITHM:
STEP 1:Read the given Data. STEP 2:Clean the Data Set using Data Cleaning Process. STEP 3:Apply Feature Encoding for the feature in the data set. STEP 4:Apply Feature Transformation for the feature in the data set. STEP 5:Save the data to the file.

FEATURE ENCODING:
Ordinal Encoding An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
Label Encoding Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
Binary Encoding Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
One Hot Encoding We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.
Methods Used for Data Transformation:
1. FUNCTION TRANSFORMATION
• Log Transformation • Reciprocal Transformation • Square Root Transformation • Square Transformation

2. POWER TRANSFORMATION
• Boxcox method • Yeojohnson method

CODING AND OUTPUT:
     import pandas as pd
df=pd.read_csv("/content/Encoding Data.csv")
df
image

ORDINAL ENCODER
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])

LABEL ENCODER
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(df[["ord_2"]])
dfc
image

dfc=df.copy()
dfc['con_2']=le.fit_transform(dfc['ord_2'])
dfc
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse_output=False)
df=df.copy()

enc=pd.DataFrame(ohe.fit_transform(df[['nom_0']]))
enc
image

df2=pd.concat([df,enc],axis=1)
df2
image

pip install --upgrade category_encoders

BinaryEncoder
image

be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb1=df.copy()
dfb
image

TARGET ENCODER
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
FEATURE ENGINEERING
image

df.skew()
image

df["Highly Positive Skew"]=np.log(df["Highly Positive Skew"])
df
image

df["Moderate Positive Skew"]=np.reciprocal(df["Moderate Positive Skew"])
df
image

POWER TRANSFORMATION
image

df["Moderate Negative Skew_yeojohnson"],parameter=stats.yeojohnson(df["Moderate Negative Skew"])
df
image

import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
image

sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
image

from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
image

RESULT:
     INCLUDE YOUR RESULT HERE
