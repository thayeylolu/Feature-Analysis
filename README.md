## Feature Analysis and Interpretation 

### Objective 
----
This report aims to interpret the importance of features of the [pumpkin seed data set](https://www.kaggle.com/datasets/muratkokludataset/pumpkin-seeds-dataset) in predicting the class of the seed (Çerçevelik or Ürgüp Sivrisi) across three machine learning algorithms: 

- Logistic Regression
- Random Forest
- Light GBM 


### The features
These are the independent features(X) of the pumpkin data set:
```area , perimeter, major_axis_length, minor_axis_length, convex_area,equiv_diameter,
eccentricity, solidity, extent, roundness, aspect_ration, compactness
```
### Feature Importance: 

#### Logistic Regression 

The coefficients and features from the logistic regression from highest to lowest magnitude: 

|Features|coefficient|magnitude|
|---------|----------|---------|
|convex_area|2.591466|2.591466|
|aspect_ration|1.785008|1.785008|
|solidity|0.703159|0.703159|
|major_axis_length|0.346242|0.346242|
|extent|0.018317|0.018317|
|minor_axis_length|-0.230135|0.230135|
|roundness|-1.034266|1.034266|
|perimeter|-1.161847|1.161847|
|equiv_diameter|-1.547765|1.547765|
|eccentricity|-1.597774|1.597774|
|compactness|-1.969038|1.969038|

According to the Logistic regression model, the `convex` feature has the highest co-efficient. **This DOES NOT** mean that it affects the model the result of the model's prediction positively. The `compactness` feature has the lowest co-efficient. This also **This DOES NOT** that it affects the model the result of the model's prediction negatively. We will put this to a test in the next section. 

### How does this affect the prediction?

From the experiment in the notebook, it was discovered that the coefficients of the model can be interpreted thus: 

- Increasing the `compactness` is likely to push the prediction towards `Çerçevelik`
- Increasing the `convex area` is likely to push the prediction towards `Ürgüp Sivrisi`
- Decreasing the `compactness` is likely to push the prediction towards `Ürgüp Sivrisi`
- Decreasing the `convex area` is likely to push the prediction towards `Çerçevelik`


#### Random Forest
The feature importance of the random forest model was found using two methods:
- The random forest `feature_importances_` method
- ELI5

**.feature_importances_ method** 
 
|Features|importance|
|---------|---------|
|aspect_ration|0.204342|
|eccentricity|0.200888|
|compactness|0.175086|
|roundness|0.106204|
|major_axis_length|0.070736|
|solidity|0.053879|
|minor_axis_length|0.042710|
|extent|0.042271|
|perimeter|0.036539|
|equiv_diameter|0.033754|


**ELI5**
|Weights|Features|
|---------|---------|
|0.2043 ± 0.4834|aspect_ration|
|0.2009 ± 0.4856|eccentricity|
|0.1751 ± 0.4416|compactness|
|0.1062 ± 0.3060|roundness|
|0.0707 ± 0.1798|major_axis_length|
|0.0539 ± 0.0288|solidity|
|0.0427 ± 0.0697|minor_axis_length|
|0.0423 ± 0.0398|extent|
|0.0365 ± 0.0478|perimeter|
|0.0338 ± 0.0230|equiv_diameter|
|0.0336 ± 0.0284|convex_area|

- Both methods ranked `aspect_ration` as the feature that affects the model's prediction the most and `equiv_diameter` as the 10th most important feature. 


### How does this affect the prediction?
From the experiment in the notebook, it was discovered that the coefficients of the model can be interpreted thus: 

- Increasing the `aspect_ration` is likely to push the prediction towards `Ürgüp Sivrisi` 
- Increasing the `equiv_diameter` is likely to push the prediction towards `Ürgüp Sivrisi`
- Decreasing the `aspect_ration` is likely to push the prediction towards `Çerçevelik`
- Decreasing the `equiv_diameter` is likely to push the prediction towards `Çerçevelik`


**Light GB: Feature Importance in Gradient Boosting Model**


##### Interpretation when class is `Çerçevelik`
- Solidity is pushing the prediction towards an higher raw score
- While compactness, aspect_ration and roundness are pushing the prediction towards a lower raw score


##### Interpretation when class is `Ürgüp Sivrisi`
- Roundness is pushing the prediction towards an higher raw score
- While compactness, aspect_ration, solidity and eccentricity are pushing the prediction towards a lower raw score
