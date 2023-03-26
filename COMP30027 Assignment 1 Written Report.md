# COMP30027 Assignment 1 Written Report

## Part 1

### Question 1

By counting true positives, true negatives, false positives, and false negatives, as well as analyzing from the confusion matrix (Fig 1), several performance metrics can be calculated. By classifying“classical”as the true label, I will report accuracy, precision, recall, and f1 score of my model. My model has an accuracy of over 97.6%, precision over 95%, a recall of 100%, and f1 score over 0.976. Such results showed my model has a strong and robust performance on classifying classical music and pop music. With over 40 test cases,  only one instance has been classified to a wrong label – a piece of pop music being classified as classical. 

<img src="https://s2.loli.net/2023/03/26/khFHG2xluQLcrDd.png" alt="pop_classical_cm" />

<center><p><i>Fig1</i></p></center> 

With a high accuracy, my model ensured over 97% of the predicted labels are correct. The high precision and perfect recall also ensures that 95% of the predicted classical music are correct and are able to detect all classical music given a dataset.

Therefore, based on the  performance metrics of my model, I am confident to make an evidential conclusion: my model yield an overall high performance on classifying pop and classical music with no bias in results. However, the model should be used with caution if an user wants to ensure all detected classical music are correct as the model might generate false positives.

### Question 2

Spectral centroid mean will be the best choice.

![Probability density of spectral centroid mean for pop and classical music](C:\Projects\COMP30027\Probability density of spectral centroid mean for pop and classical music.png)

<center><p><i>Fig2</i></p></center> 

![Probability density of harmony mean for pop and classical music](https://s2.loli.net/2023/03/26/PsFmeVQNw9K8MZE.png)

<center><p><i>Fig3</i></p></center> 

![Probability density of tempo for pop and classical music](https://s2.loli.net/2023/03/26/furEi1SsYQbDgGx.png)

<center><p><i>Fig4</i></p></center> 

From the above graphs (Fig 2, Fig 3, Fig 4), it is clearly visible that Fig 2 has the minimal probability density function (pdf) overlap between two classes, where as the other two features has a high overlap in pdfs. The overlap of the pdf can create potential errors: although the probability of a class is higher, the probability of the other class still present. For example, in Fig. 4, since the probability of an instance being a pop music is higher between tempo=60 and tempo=140, the model will classify the instance as pop. However, although the probability of pop is high, the probability of the instance being a classical music is not low as well. In this case, if we are only classifying instances using tempo, it is likely that a number of classical instances will be classified as pop, generating false positives. On the contrary, in Fig. 2, there are only overlaps  between SCM=1500 and SCM=2000, which only consists a very small proportion of the range of the feature.

Therefore, choosing SCM will yield a better performance of the model as classes are more disguisable resulting in less potential errors.

## Part 2

### Question 6

The model is tested from 0% missing value (the original test data) to 90% missing data. The results are as follows:

![Accuracy with different missing data amount](https://s2.loli.net/2023/03/26/T4hcnsLDJvw37jY.png)

<center><p><i>Fig5</i></p></center> 

![Precision with different missing data amount](https://s2.loli.net/2023/03/26/SCAbntmzVv96WPU.png)

<center><p><i>Fig6</i></p></center> 

![Recall with different missing data amount](https://s2.loli.net/2023/03/26/F9hyd53lpSQjImO.png)

<center><p><i>Fig7</i></p></center> 

From graphs and table above, it is notable that the Naïve Bayes model’s performance varies between the amount of missing data. When the amount of missing data is low (i.e. from 10% to 20%), the overall performance remained roughly the same as when there are no missing data. This showed the robustness of the Naïve Bayes model – even if there are some missing data in the dataset, the model can still make predictions stably. 

When the amount of missing data increased to between 30% to 40%, the model’s performance, however, increased, and by all metrics. I suspect this result is due to distributions of the features. Since the Naïve Bayes model I implement  assumes all features are in gaussian distribution in both datasets, but this might not be the reality since we didn’t validate before training and testing. However, during the random deletion of data,  the test data might have turned into a gaussian distribution, resulting in a better performance. 

When the amount of missing data is high (i.e >= 50%), the performance of the model dropped massively, especially when the amount of missing data is extremely high (i.e. 80% - 90%). I suspect this is a result of a few or one feature dominates the prediction. In this case the one feature or the very few features that dominates the prediction might lead to high error rates as there might be high overlaps between pdfs of different classes as discussed in Q2. 

Overall, the Naïve Bayes model remains robust against low to moderate level of missing data, but performs poorly in higher levels of missing data.