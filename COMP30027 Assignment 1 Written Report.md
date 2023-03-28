# COMP30027 Assignment 1 Written Report

## Part 1

### Question 1

By counting true positives, true negatives, false positives, and false negatives, as well as analyzing from the confusion matrix (Fig 1), several performance metrics can be calculated. By classifying“classical”as the true label, I will report accuracy, precision, recall, and f1 score of my model. My model has an accuracy of over 97.6%, precision over 95%, a recall of 100%, and f1 score over 0.976. Such results showed my model has a strong and robust performance on classifying classical music and pop music. With over 40 test cases,  only one instance has been classified to a wrong label – a piece of pop music being classified as classical. 

<img src="https://s2.loli.net/2023/03/26/khFHG2xluQLcrDd.png" alt="pop_classical_cm" />

<center><p><i>Fig. 1</i></p></center> 

With a high accuracy, my model ensured over 97% of the predicted labels are correct. The high precision and perfect recall also ensures that 95% of the predicted classical music are correct and are able to detect all classical music given a dataset.

Therefore, based on the  performance metrics of my model, I am confident to make an evidential conclusion: my model yield an overall high performance on classifying pop and classical music with no bias in results. However, the model should be used with caution if an user wants to ensure all detected classical music are correct as the model might generate false positives.

### Question 2

Spectral centroid mean will be the best choice.

![Probability density of spectral centroid mean for pop and classical music](C:\Projects\COMP30027\Probability density of spectral centroid mean for pop and classical music.png)

<center><p><i>Fig. 2</i></p></center> 

![Probability density of harmony mean for pop and classical music](https://s2.loli.net/2023/03/26/PsFmeVQNw9K8MZE.png)

<center><p><i>Fig. 3</i></p></center> 

![Probability density of tempo for pop and classical music](https://s2.loli.net/2023/03/26/furEi1SsYQbDgGx.png)

<center><p><i>Fig. 4</i></p></center> 

From the above graphs (Fig 2, Fig 3, Fig 4), it is clearly visible that Fig 2 has the minimal probability density function (pdf) overlap between two classes, where as the other two features has a high overlap in pdfs. The overlap of the pdf can create potential errors: although the probability of a class is higher, the probability of the other class still present. For example, in Fig. 4, since the probability of an instance being a pop music is higher between tempo=60 and tempo=140, the model will classify the instance as pop. However, although the probability of pop is high, the probability of the instance being a classical music is not low as well. In this case, if we are only classifying instances using tempo, it is likely that a number of classical instances will be classified as pop, generating false positives. On the contrary, in Fig. 2, there are only overlaps  between SCM=1500 and SCM=2000, which only consists a very small proportion of the range of the feature.

Therefore, choosing SCM will yield a better performance of the model as classes are more disguisable with this feature and will result in less potential errors.

## Part 2

### Question 6

The model is tested from 0% missing value (the original test data) to 90% missing data, with 3 iterations with different random seeds. Results are as follows:

![Accuray_agg](https://s2.loli.net/2023/03/27/bpIJ2UgFLVGfqlv.png)

<center><p><i>Fig. 5</i></p></center> 

![Precision_agg](https://s2.loli.net/2023/03/27/rIAbdtG9y1ksNfv.png)

<center><p><i>Fig. 6</i></p></center> 

![Recall_agg](https://s2.loli.net/2023/03/27/xU2B9j3DhGi5raZ.png)

<center><p><i>Fig. 7</i></p></center> 

![avg_me_agg](https://s2.loli.net/2023/03/27/31YdgBNbIz5MCnK.png)

<center><p><i>Fig. 8</i></p></center> 

From graphs above, it’s notable that the Naïve Bayes model’s performance in all metrics varied between the amount of missing data. During each iteration, though variations present, performance of the model showed a same trend as the averages in all metrics: the model’s performance slightly increases when there are small number of missing values, but decreases when the number of missing values increase from then on, especially when the number of missing values is extremely high (i.e. 80% and 90%). 

The increase in performance with low missing data percentage could be a result of a removal of dependent attributes and removal attributes that has high error rate. Since my model is a gaussian Naïve Bayes model, the model assumes data are in gaussian distribution and are independent from each other. However, such assumptions might not hold in out dataset as no checking has been done. With some features being randomly removed, some coupled features might be broken up, resulting in independency between features and no attributes being overweighed. Another reason could be attributes that has high pdf overlaps between classes was removed, resulting the model having a better performance as discussed in Q2.

The dramatic decrease in performance with high missing value rates could be a consequence of lacking information. With 80% - 90% of features removed, the model is inferencing results basing on only one to two attributes. However, those features could be misleading and there are no other features to balance out that feature, causing poor performance.

Overall, a Naïve Bayes model is robust against low to moderate level of missing values, but will perform poorly when there are large number of missing values.