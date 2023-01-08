## Foreign university admission prediction

### Business Case: Jamboree Education - Linear Regression

#### Problem Statement:

Jamboree has helped thousands of students like you make it to top colleges abroad. Be it GMAT, GRE or SAT, their unique problem-solving methods ensure maximum scores with minimum effort.

They recently launched a feature where students/learners can come to their website and check their probability of getting into the IVY league college. This feature estimates the chances of graduate admission from an Indian perspective.

Your analysis will help Jamboree in understanding what factors are important in graduate admissions and how these factors are interrelated among themselves. It will also help predict one's chances of admission given the rest of the variables.

#### Solution: EDA | ML model building

Jamboree has helped thousands of students make it to top colleges abroad. Be it GMAT, GRE or SAT, their unique problem-solving methods ensure maximum scores with minimum effort. They recently launched a feature where students/learners can come to their website and check their probability of getting into the IVY league college. This feature estimates the chances of graduate admission from an Indian perspective.

As per the business problem, the company wants to know what factors are important in graduate admissions and how these factors are interrelated among themselves. It will also help predict one's chances of admission given the rest of the variables.

It was a simple data frame which consisted of different students educational profile in each row along with their chance of admission. I found the data very clean and properly structured. There were no missing values found. There were no duplicate rows found. I found little to no outliers in any of the features. 

With the given data, I was able to draft certain observations which can help Jamboree education in their growth as a company. I also created a linear regression model which can predict the Chance of a student's admission with the help of the data set given.

1. I started with the basic EDA. The data set which was given to us had all the values with data types either as an integer or float. Chance of Admit was the target or dependent variable. The rest were independent features. The independent features reflected the educational background and metrics of 500 different students. 
2. University Rating, SOP, LOR and Research were considered as ordinal categorical variables as they had unique values which were less than 10. Gre, toefl scores, CGPA and chance of admit were considered as continuous variables. GRE and TOEFL are the only features which the Jamboree can help  
3. Plotted histogram and KDE of each and every independent features. All the continuous features almost followed a normal distribution. GRE and TOEFL scores are the only features which the Jamboree can control. 
Starting with GRE score, I could see that the count of the students from 310 to 330(considering 310 as an ideal or good score) is the highest. Still there are many students below 310 which might affect the Jamboree's reputation. Hence, I would advise the management and faculty team to focus more on the people who have scored less than 310. By opening a separate batch to retrain them and give exams again might help with their scores. Toefl scores has good number of students above 100, but it would be even better if we try to reduce the number of students who are getting below 100. 
4. I also plotted a scatter plot between the target variable and the independent features. I could clearly see an increasing trend. Since all features are either ordinal discreet or continuous, higher the value of independent features, greater is the chance of a student's admission. 
5. I plotted a heat map to check Pearson correlation between the independent features. Higher correlation  was observed in CGPA vs TOEFL Score, CGPA vs GRE score and TOEFL vs GRE. Hence, higher the CGPA, higher is the GRE or Toefl scores.  Hence, even before starting the classes, we can allot different classes or training structures (focussing more on students with lesser CGPA) for different students, so that our minimum is a good GRE or TOEFL score. 
6. Also, I checked correlation of each independent feature with target variable. I could see that CGPA, GRE and TOEFL were among the top three. Since, CGPA is something we cannot control, to increase their chances of admit, GRE and TOEFL scores play a very important role. 
7. I then started with my LR model. Since, the ranges of GRE and TOEFL scores were very high as compared to other features, I had to scale the entire data frame. I used min-max scaling for this. I could bring down all the values in the range of [0,1]. I, then created train and train data sets. (80 % & 20% of df). 
8. Used statsmodel API to train a basic LR model. Given below is the inference from the summary. 
   * R2 and adj. R2 for our training data came out to be 0.821 and 0.818 respectively. (We cannot come to any conclusion unless we predict using our test data)
   * Checking statistical signficance of the coefficients using t-test statistic.
     * ==> Null hypothesis: A coefficient is almost close to zero.
     * ==> Alternate Hypothesis: A coefficient is non-zero.
   * Let significance level α = 5% or p-val = 0.05
   * We can see that only university rating and SOP features have pval > 0.05 and their t-statistics are almost close to 0.
   * Hence, we fail to reject null hypothesis thereby concluding university rating and SOP has almost no significance on target variable.
   * Though we see that other features are statistically significant, there might be MultiCollinearity amongst them.
9. When, I predicted the same model on test data set, I got the r2 score around 0.81 which was really good. 
10. Even though there was not much variance between r2 scores of 0.82 and 0.81. I still went ahead and tried to optimise my model. Cross validation(CV) was very important in this case, as we need a separate part of data set for validation. Since, the number of data points were very less, I had to go with k fold validation. 
11. I added extra polynomial features to see if I can get an extra score on training data and CV data sets. After running a loop from 1 to 5 degree, I came up with a conclusion that degree 1 is the best which is linear.
12. To avoid overfitting or to get a best fit(medium bias and variance), I went with L2 regularization or ridge regression. Hyperparameter tuning was done to get the best possible alpha or lambda value. The highest r2 score came out for lambda value of 1. I got 0.81 again for test scores which is the best fit in my opinion. 
13. All the assumptions of the linear regression model were also tested. Except VIF check, all the other assumptions came out to be almost true. Even though, almost all the features had VIF scores greater than 5, we cannot just drop the features to avoid multicollinearity as that would greatly affect the performance of our model. 
14. Even though 0.81 is a very good test score for an ML model, there are chance where we might get more errors once it is deployed in the real world. The features and number of data points which were used were very less. We can try to add more features to the model like mock test scores,  work experience etc, which can add great value to the model and give better predictions in the real world. To improve our performance even more, we need to train our model at least on 100, 000 data points, to give correct predictions right from the go. 

To whoever reads this, I hope my insights and recommendations from this case study were meaningful.

Thank you,

Krishna