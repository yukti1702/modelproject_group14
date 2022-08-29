Modelproject_group14

Basic information
•	Person or organization developing model : Yukti Handa, yhanda11@gwu.edu
•	Model date: August, 2022
•	Model version
•	License
•	Model implementation code

Intended Use
•	Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase.
•	Primary intended users: Students in GWU DNSC 6301 bootcamp.
•	Out-of-scope use cases: Any use beyond an educational example is out-of-scope.
 


● Training data:
○ Source of training data: GWU Blackboard, email  'yhanda11@gwu.edu' for more information
○ How training data was divided into training and validation data: 50% training data, 25% validation data, 25% test data
○ Number of rows in training and validation data: 15,000 training rows; 7,500 validation rows
○ Data dictionary; for each column in the training dataset include: 
■ Name
■ Modeling role
■ Measurement level
■ Description

● Test data:


Source of test data:- credit_line_increase.csv,GWU Blackboard, email  'yhanda11@gwu.edu' for more information
 Number of rows in test data:- 7500 rows 
State any differences in columns between training and test data- None
 


● Model details:
○ Columns used as inputs in the final model
 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'


○ Column(s) used as target(s) in the final model
'DELINQ_NEXT'

○ Type of model
 Decision Tree Classification

○ Software used to implement the model
Python, scikit-learn

○ Version of the modeling software
Python version: 3.11 
sklearn version: 1.0.2

○ Hyperparameters or other settings of your model
DecisionTreeClassifier( max_depth=12, random_state=SEED)


● Quantitative analysis:
○ Metrics used to evaluate your final model (AUC and AIR)
○ State the final values, neatly -- as bullets or a table, of the metrics for all data:
training, validation, and test data
○ Provide any plots related to your data or final model -- be sure to label the plots!


Metrics used to evaluate your final model: AUC and AIR
Training AUC: 0.7837
Validation AUC: 0.7496
Test AUC: 0.7438
AIR in Bias testing:
hispanic-to-white AIR:  0.76
black-to-white AIR:  0.82
asian-to-white AIR:  1.00
female-to-male AIR:  1.06
AIR in Bias Remediation:
hispanic-to-white AIR:  0.83
black-to-white AIR:  0.85
asian-to-white AIR:  1.00
female-to-male AIR:  1.02

Plots related to model training

The histograms for all the columns in the data:


We can intuitively detect the group attribute bias in our data—young, single, highly educated women from the histogram. Additionally, each variable's data distribution is visible. For instance, we discovered that in DELINQ NEXT,  the number of people who paid on time far exceeded those who delayed. Comparing the outcomes with the training data is useful.
Correlation Heatmap

The heatmap shows the corresponding colors between the variables are dark and light. The link between the variables is stronger when the color area is lighter, which indicates that the variables interact with one another. Conversely, when the color area is darker, the interaction between the variables is weaker.
According to the figure, “history of past payment” has a certain influence on our target variable(DELINQ_NEXT), while race has almost no effect on the result of the target variable.

Iteration Plot （Training the model by decision tree）:



The AUC indicator is used to assess the level of model learning by feeding the model training set and validation set, and the aforementioned figure is produced. We can see intuitively from the plot function that the model learns most well when the tree depth is 6, which allows us to define the model's training parameters as 6.

Decision Tree:（Draw a decision tree with a depth of 6）

 
Variable Importances:

The variables are sorted by importance by the importances.sort_values() function. The range of variables influencing the target variable (DELINQ NEXT) is down to pay_0, as seen in the figure (the repayment status in September).

Final Iteration Plot with AIR:



To retrain the model with the additional data (race and sex), we were able to obtain the necessary AIR value (greater than 0.8). As seen in the figure, we can see that the model with a tree depth of 6 works well by combining the indicators of AUC and AIR.


● Ethical considerations:

■ Math or software problems

The results of using a model is simply a measure, there is not a way to account for bias. Naturally, bias is built into a model and may lead to the model missing any relevant relationships between data inputs and the predictions. The model is very dependent on the status of the immediate payment, this could negatively impact the model depending on an individual's previous payment history. 

Using a decision tree model creates a biased tree due to the dominance of certain categories, which affects the accuracy of the target variable. Therefore, we should balance the data before fitting it with a decision tree model, addressing the so-called bias problem from the outset.

We found that in our model, the hyperparameters class_weight and max_leaf_nodes are all none, which will cause the data volume of the leaf nodes to be too large or too small, so that the data cannot be summarized well, thus affecting the prediction results of the next layer of leaf nodes. 

 ■ Real-world risks: who, what, when or how

Because the decision tree model relies too much on the “pay 0” variable in the data (that is, the last repayment status), this is not in line with real life. For example: I have repaid and paid off the loan several times before, but only recently failed to repay the loan on time by accident. According to the logic of the decision tree model, I cannot enjoy the increase in credit card limit. Then there will be people who only choose to pay off the bill on time for the last time in order to obtain a credit card with a higher limit.

The results of using a model is simply a measure, there is not a way to account for bias. Naturally, bias is built into a model and may lead to the model missing any relevant relationships between data inputs and the predictions. The model is very dependent on the status of the immediate payment, this could negatively impact the model depending on an individual's previous payment history. 




