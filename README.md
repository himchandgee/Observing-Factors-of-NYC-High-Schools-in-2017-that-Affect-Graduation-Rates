# **Introduction** and Objectives

Data Set Name: 2017 DOE High School Directory

Data Set Link: [https://data.cityofnewyork.us/d/s3k6-pzi2](https://data.cityofnewyork.us/d/s3k6-pzi2) Currently Not Working

Objective: Find a data model that will utilize different aspects of a high school to determine whether the school will have a low, medium, or high graduation rate.

Data Set Description:

The data we are using is information on New York high schools, their academic programs, and various statistics about the students. The data goes over attendance rates, the total number of students, graduation rates, and the programs the schools provide. They also have information on school locations, contacts, and campus type. Each school has an overview paragraph to explain its goals and the programs it offers.  Additionally, it includes information on each school’s ELL (English as a New Language) programs, language classes, and extracurricular opportunities.

Data Mining Methods: 

For the Data Mining task, we'll use logistic regression, random forest, and gradient boosting to create a reliable model to determine what features are important for school graduation rates. Logistic regression will provide each considered attribute’s coefficient after training the model, providing a look at which attributes matter more to the model. Random forest allows us to decide which features are more impactful by dividing them into Decision Trees. More impactful features will result in more consistent results when determining graduation rates. Gradient boosting is another model that will provide us with similar information and provides us with another option to compare our results to. Furthermore, it is a more robust model that, if shown to be more accurate than our other models, would be a good starting place to implement more attributes to improve classification. 




# Data Cleaning

To clean the data for our objective, we removed rows of data that didn’t include a graduation rate. Next, for the logistic regression, the Scikit-Python library was utilized to fill in empty values for our independent variables, including total_students, attendance_rate, college_career_rate, pct_stu_safe, and pct_stu_enough_variety. Using the same library, we standardized all the values across our numeric data to ensure our data was implemented at the same scale, so that values like total_students wouldn’t trump attendance_rate. For the random forest model, we filled empty values in the independent variables with 0. Finally, for the gradient boosting model, we just removed any columns with missing data in our independent variables. Furthermore, we binned each school’s graduation rates into low, medium, and high, with the ranges ≤ 0.6, 0.6-0.8, and 0.8 ≥ respectively.


# Attribute Selection

For our logistic regression algorithm, we chose mostly numeric data to see how the traits that every high school would have would affect the graduation rate of students. Total number of students (total_students), their overall attendance rate (attendance_rate), the rate of students moving on to higher education (college_career_rate), the percent of students that felt safe within their school (pct_stu_safe), and the percent of students that felt their school offered enough variety in classes and activities to keep them interested (pct_stu_enough_variety) are all things that are good markers for the quality of a school, leading to their corresponding graduation rate. Any new school introduced into the NYC DOE system would have many of these general traits, and using their numerical data for these traits could help determine their graduation rate and help administrators figure out what areas to improve.


# Data Training

To train our data for the logistic regression, the Pipeline class from the scikit library takes our data and finds the best weight for each of our independent variables for each class. It produces coefficients for each variable that represent the weight of how much they affect the classification of each row of data. We decided on using 80 percent of the data for training the model and 20 percent of the data, after cleaning, for testing the model.


# Results


## Logistic Regression



<img width="520" height="455" alt="image5" src="https://github.com/user-attachments/assets/86e11422-a365-4411-adde-373b89484d72" />





<img width="524" height="243" alt="image2" src="https://github.com/user-attachments/assets/8a2031a9-1086-4dfb-a2ee-81b91cc00b0d" />




Our logistic regression model did particularly well in predicting schools with high graduation rates, but struggled with predicting schools with low graduation rates.  Low graduation rate schools are often misclassified as medium graduation rate schools. This makes it difficult for this model to be used to detect schools having trouble with their students’ performance. The model's overall accuracy is 74%, which could be improved by considering more attributes in the data.


<img width="747" height="251" alt="image1" src="https://github.com/user-attachments/assets/3c512aed-46b4-4dc7-ab61-bf547c5883d0" />



Among the attributes that were considered, attendance_rate and college_career_rate had the most weight in determining a high graduation rate school, meaning that high attendance and more college preparation provided by the school resulted in higher graduation rates. The inverse is true for schools with low graduation rates, showing that low attendance and lack of college preparation lead to low graduation rates.


## Random Forest Model


<img width="409" height="209" alt="image8" src="https://github.com/user-attachments/assets/607e5c16-ab06-43ba-a0f4-54bca6714798" />



The Random Forest Model is a decently accurate predictive model that can determine the graduation rate. Using this model, we've determined that it can predict high graduation rates more accurately than low graduation rates, with high graduation rates having a ninety-seven percent precision, low graduation rates having a thirty-eight percent precision, and middle rate graduation rates having a seventy percent precision.

<img width="520" height="455" alt="image7" src="https://github.com/user-attachments/assets/04fe5a8e-f467-48b8-8e88-39a546bc6801" />




To ensure that the data is consistent throughout retesting the mode, it uses an N estimator of 100 when creating the random forests and uses a specific random state when splitting data to ensure that the result can be replicated. To accurately determine the importance of each feature, we created a chart to determine the importance and weight of each feature.


<img width="989" height="590" alt="image9" src="https://github.com/user-attachments/assets/a1a65a5b-fabe-4d3e-84e7-5ea61b788082" />


To determine the important features, we used the feature importance calculator, and we discovered that college career rates had the highest importance, followed by attendance rates, along with student safety. Using this, we determined that the total number of students and the variety of programs offered don't have much of an effect on graduation rates.


## Gradient Boosting Model 


<img width="520" height="455" alt="image3" src="https://github.com/user-attachments/assets/4a2a54b8-0a53-46dc-b664-9b15961efe7b" />


<img width="527" height="242" alt="image6" src="https://github.com/user-attachments/assets/f0f74234-6fd3-489d-a8b1-b969ed8c1a56" />


The gradient boosting model produced similar results to our other models, predicting high graduation schools better than medium and low graduation rate schools. Low graduation rate schools were still being mistaken half of the time for medium graduation rate high schools. Out of our three models, the gradient boosting model had the lowest performing accuracy, though the difference is small and only a few percent.


<img width="989" height="590" alt="image4" src="https://github.com/user-attachments/assets/c188bb54-b64c-48dc-b71a-7690eaa811ac" />


The gradient boosting model valued the college_career_rate attribute a lot more than other attributes, which differs from our other models. Our other models do value college_career_rate highly, but attendance_rate would not have such a high difference in importance compared to college_career_rate. Using this model would lead to the interpretation that schools with lower graduation rates could improve their rates solely by having more college preparation for students. While this would help, I don’t think this model accurately depicts the value of the other attributes.


# Conclusion and Future Works

In conclusion, out of the three models that we ran our data through, the random forest model performed the best with a 75% accuracy. With the results of the three models, we determined that the attendance rate and proper college preparation provided by the school play large roles in making a school successful, with the graduation rate as the mark of success. 

To improve our models in the future, we would include more attributes within our data, such as AP courses and languages taught at each school. Furthermore, we would use text filtering on some of the attributes in our data to determine the school’s main program that they focus on, and find some of the most successful kinds of programs that lead to higher graduation rates. Furthermore, our results could be better produced with more consistency across all our models' data, such as making sure that all of our data was cleaned in the same way.


# Team Contributions

Ivan Yu:

I produced the code for the logistic regression and gradient boosting models. I wrote the data cleaning, attribute selection, a majority of the data training, logistic regression, gradient boosting, conclusion, and future works sections of the report. 

Himchand Gee:

I worked on code for creating the random forest model and for dividing up the data in our Jupyter Notebook. I also helped troubleshoot some of the code because of an issue with the separation of training data and testing data.
