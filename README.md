# Madelon-Data-Set

>Nous l'appelons la Madelon
>Nous en rêvons la nuit, nous y pensons le jour,
>Ce n'est que Madelon mais pour nous c'est l'amour

The Madelon Data Set can be acquired [here](http://archive.ics.uci.edu/ml/datasets/madelon) from the UCI Machine Learning Repository.

A summary of problem statement is defined below:

1.  Domain:  Artificial
2.  Problem Statement:  Classify Random Data (Training, Validating, Testing)
3.  Description of Data Set:  500 Features, Random, Dense, Bimodal
4.  Proposed Solution:  Kernel Methods and SVMs
5.  Benchmark Model:  Logistic Regression
6.  Performance Metrics:  BER and AUC


## 1. Domain

#### Real World Source
The Madelon dataset is unique in that is it an artifical data set. It was included as one of 5 datasets in the 2013 Neural Information Processing Systems (NIPS) feature selction challenge. 

The dataset is was donated in 2008 by Isabele Guyon. The values were generated via hypercube_data.m, a MATLAB program. The premise in designing the set was 20 real features and 480 'probes' with no predictive power as distractors under a N(0,1) distribution. The challenge exists in classifying the data into +1 and -1 when no feature is informative by itself. 

#### Literature Review


Information regarding the construction and MATLAB code of the dataset can be found in the Dataset E section in [Design of experiments for the NIPS 2003 variable selction benchmark](https://archive.ics.uci.edu/ml/machine-learning-databases/madelon/Dataset.pdf). 


Additonal resources by the same author and all around cool lady with a very basic html website, [Isabelle Guyon](http://www.clopinet.com/isabelle/).


Isabelle Guyon, et al, 2007. Competitive baseline methods set new standards for the NIPS 2003 feature selection benchmark. Pattern Recognition Letters 28 (2007) 1438–1444. 
and the associated technical report: 
Isabelle Guyon, et al. 2006. [Feature selection with the CLOP package.](http://clopinet.com/isabelle/Projects/ETH/TM-fextract-class.pdf) Technical Report. 

Surprisingly, the "Madelon Dataset" has a mere 7k hits on a Google Search, which probably means it exists in some obscurity. The 80-20 rule is probably an apt description in that the minority (20%) of those who know the data set understand 80%, while the majority (80%) who have heard of it may only understand 20%. Whichever the case, perhaps by the end of this project, we will be in the minority. 



## 2. Problem Set

>'One dataset (Madelon) was artifically constructed to illustrate a particular difficulty: selecting a feature set when no feature is informative by itself.'

#### Inputs

The dataset consists of a training set, a validation set, and a test set. Each set consists of 500 non-descript features, with 20 real features and 480 probes to add noise. The training set is provided with labels, while the validation set and test set have the labeled +1 -1 values withheld.


#### Type of Data Science or Machine Learning
This is a two part problem.
1. *Binary Classification* The input data consists of 500 non-descript features which will be mapped via a  classification model onto either discrete value of +1 or -1. 
2. *Feature Selection* Part of the problem is identifying the 20 relevant features (5 informative, and 15 repetitive) from the 'probes' (480 features) which add noise to the dataset. 


#### Outputs

The output is sorting the data into two classes corresponding to the labels. The train_data.labels consists of a file with the corresponding +1 or -1 label for each example. 


## 3. Description 

The parameters of the dataset are provided in madelon.param file. 

Data type: non-sparse
Number of features: 500
Number of examples and check-sums:

| --- | Pos_ex | Neg_ex | Tot_ex | Check_sum |
| --- | --- | --- | --- | --- |
| Train | 1000 | 1000 | 2000 | 488083511 |
| Valid | 300 | 300 | 600 | 146395833 |
| Test | 900 | 900 | 1800 | 439209553 |
| All | 2200 | 2200 | 4400 | 1073688897 |

Further description, visualization, and memory usage of the data is available in the .ipynb file.
Nonsparse indicates that absence of NULL values in the dataset. Values are of numeric type.

Data on the data sets, their dimensions, and memory usage follow:
| Set | Dimensions | Memory (in MB) |
| --- | ---| --- |
| Training Set | 2000 x 500 | 6.9 |
| Validation Set | 599 x 500 | 1.2 |
| Test Set | 1800 x 500 | 3.5 | 
| Labels | 2000 x 1 | 0.0085 |

Generating summary statistics for the group does ot make the most intuitive sense (mean, median, mode, types), since the features themselves do not reveal information regarding the set. 


## 4. Solution


According to the organizers of the 2003 NIPS challenge, in "Result Analysis" below, kernel methods "are most popular" for approaching the classification problem, and most kernel methods were SVMs.  For *Madelon* specifically, "all best ranking groups used a Gaussian kernel."
Training and testing a variety of methods and models, for both feature selection and classification, will be the route most likely to provide a satisfactory solution.  What those particular methods and models will be is unknown at this point.


## 5. Benchmark Model

Since the data is binary classification into +1 and -1, a simple measure of accuracy would be insufficient in establishing a base success, as probablity dictates 50% accuracy rate, which is no more than a simple dice roll. 

Instead, a logistic regression model will be used as the benchmark because it is a simple and common classification which will provide a base line to measure more sophisticated models against.

![Logistic Regression](https://upload.wikimedia.org/wikipedia/commons/8/88/Logistic-curve.svg)
...but in 5 dimensions. 


## 6. Performance Metric

As we have a binary classification, [various performance metrics](https://turi.com/learn/userguide/evaluation/classification.html) can be used to evaluate the performance of our model. 

An F-score based on precision and recall may not be the best metric as there is no way to assign empirical meaning to the resulting false positive and false negatives in an artifical data set (as opposed to a diagnosis classification). 
![Precision and Recall](https://commons.wikimedia.org/wiki/File:Precisionrecall.svg#/media/File:Precisionrecall.svg). 

The "Result Analysis" suggests the use of the balanced error rate (BER) and area under the ROC curve (AUC) as appropriate performance metrics.  Since *Madelon* results in a binary output, the "Results Analysis" considered BER = 1 - AUC.
Other considerations are the fraction of features selected and the fraction of probes found in the feature set selected.

![BER and AUC](https://upload.wikimedia.org/wikipedia/commons/4/4f/ROC_curves.svg)
The AUC of the diagonal line represents the 'coin flip' or 50:50 distribution, whereas the curved line would be the performance of our logistic regression model. The closer the curve banks to the upper left, the greater the AUC (and consequently lower the BER).

