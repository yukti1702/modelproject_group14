### Modelproject_group14

### Basic information:

* 	Person or organization developing model : Yukti Handa, yhanda11@gwu.edu 
* 	Model date: August, 2022 
* 	Model version: 1
* 	License: MIT
* 	Model implementation code: modelproject_group14.ipynb
* 	### Intended Use 
    *  __Primary intended uses__ : This model is an example probability of default classifier, with an example use case for determining eligibility for a credit line increase. 
    * 	__Primary intended users__: Students in GWU DNSC 6301 bootcamp. 
    * 	__Out-of-scope use cases__: Any use beyond an educational example is out-of-scope.

### Training data:

* 	__Source of training data__: GWU Blackboard, email  'yhanda11@gwu.edu' for more information
* 	__How training data was divided into training and validation data__: 50% training data, 25% validation data, 25% test data
* 	__Number of rows in training and validation data__: 15,000 training rows; 7,500 validation rows
* __Data dictionary__: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

### Test data

 * __Source of test data__:- credit_line_increase.csv,GWU Blackboard, email  'yhanda11@gwu.edu' for more information
 * __Number of rows in test data__:- 7500 rows 
 * __State any differences in columns between training and test data__:-None

### Model details:

* **Columns used as inputs in the final model**: &#39;LIMIT_BAL&#39;,
&#39;PAY_0&#39;, &#39;PAY_2&#39;, &#39;PAY_3&#39;, &#39;PAY_4&#39;, &#39;PAY_5&#39;, &#39;PAY_6&#39;, &#39;BILL_AMT1&#39;,
&#39;BILL_AMT2&#39;, &#39;BILL_AMT3&#39;, &#39;BILL_AMT4&#39;, &#39;BILL_AMT5&#39;, &#39;BILL_AMT6&#39;,
&#39;PAY_AMT1&#39;, &#39;PAY_AMT2&#39;, &#39;PAY_AMT3&#39;, &#39;PAY_AMT4&#39;, &#39;PAY_AMT5&#39;, &#39;PAY_AMT6&#39;
* **Column(s) used as target(s) in the final model**: &#39;DELINQ_NEXT&#39;
* **Type of model**: Decision Tree
* **Software used to implement the model**: Python, scikit-learn
* **Version of the modeling software**: Python version: 3.11, sklearn version: 1.0.2
* **Hyperparameters or other settings of your model**:
```
  DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion=&#39;gini&#39;,
  max_depth=6, max_features=None, max_leaf_nodes=None,
  min_impurity_decrease=0.0, min_impurity_split=None,
  min_samples_leaf=1, min_samples_split=2,
  min_weight_fraction_leaf=0.0, presort=&#39;deprecated&#39;,
  random_state=12345, splitter=&#39;best&#39;)
```
  
### Quantitative analysis:
* **Metrics used to evaluate your final model: AUC and AIR
* Training AUC: 0.7837
* Validation AUC: 0.7496
* Test AUC: 0.7438
* AIR in Bias testing:

| hispanic-to-white AIR |black-to-white AIR | asian-to-white AIR | female-to-male AIR |
| ------ | ------- | -------- | -------- |
| 0.76 | 0.82 | 1.00 | 1.06 |

* AIR in Bias Remediation:

| hispanic-to-white AIR |black-to-white AIR | asian-to-white AIR | female-to-male AIR |
| ------ | ------- | -------- | -------- |
| 0.83 | 0.85 | 1.00 | 1.02 | 

### Plots related to model training
#### The histograms for all the columns in the data

We can intuitively detect the group attribute bias in our data—young, single, highly educated women from the histogram. Additionally, each variable's data distribution is visible. For instance, we discovered that in DELINQ NEXT,  the number of people who paid on time far exceeded those who delayed. Comparing the outcomes with the training data is useful.

![图片1](https://user-images.githubusercontent.com/111601038/187104499-a8dfbabf-bfc4-4f20-84f0-6b01dae28ae0.png)
![图片2](https://user-images.githubusercontent.com/111601038/187104504-a6d73eba-d3a5-4327-ae84-97c0151be251.png)

#### Correlation Heatmap

The heatmap shows the corresponding colors between the variables are dark and light. The link between the variables is stronger when the color area is lighter, which indicates that the variables interact with one another. Conversely, when the color area is darker, the interaction between the variables is weaker.
According to the figure, “history of past payment” has a certain influence on our target variable(DELINQ_NEXT), while race has almost no effect on the result of the target variable.

![图片3](https://user-images.githubusercontent.com/111601038/187104514-c89cb505-0d8d-4095-9af0-321a0749aebe.png)

#### Iteration Plot （Training the model by decision tree）:


The AUC indicator is used to assess the level of model learning by feeding the model training set and validation set, and the aforementioned figure is produced. We can see intuitively from the plot function that the model learns most well when the tree depth is 6, which allows us to define the model's training parameters as 6.

![图片4](https://user-images.githubusercontent.com/111601038/187104539-61c0f73f-17c0-40bd-803f-2c8c8a682f6c.png)

#### Decision Tree:（Draw a decision tree with a depth of 6）

![下载](https://user-images.githubusercontent.com/111601038/187104693-404d00ae-155a-4779-a8e6-b46c3f55adfb.png)

#### Variable Importances:

The variables are sorted by importance by the importances.sort_values() function. The range of variables influencing the target variable (DELINQ NEXT) is down to pay_0, as seen in the figure (the repayment status in September).

![图片5](https://user-images.githubusercontent.com/111601038/187104554-b987660d-17ce-48ef-84ec-057e3a77c690.png)

#### Final Iteration Plot with AIR:

To retrain the model with the additional data (race and sex), we were able to obtain the necessary AIR value (greater than 0.8). As seen in the figure, we can see that the model with a tree depth of 6 works well by combining the indicators of AUC and AIR.

![图片6](https://user-images.githubusercontent.com/111601038/187104562-8107a413-0f8f-4c28-b9f8-df849e9834c5.png)

### Ethical considerations:

■ **Math or software problems**

There is no way to take bias into account when employing a model; the findings are just a metric. A model will inevitably have bias, which could cause it to ignore any important connections between the data inputs and the predictions. The model depends heavily on the status of the immediate payment; depending on the individual's past payment behaviour, this could have a negative effect.

Because of the dominance of some categories in a decision tree model, the accuracy of the target variable is impacted. Therefore, in order to address the so-called bias problem from the outset, we need balance the data before fitting it with a decision tree model.We discovered that our model's class weight and max leaf nodes hyperparameters are all zero, which would make the leaf nodes' data volumes either too large or too small, making it difficult to summarize the data effectively and impacting the prediction outcomes of the subsequent layer of leaf nodes.

 ■ **Real-world risks: who, what, when or how**

This is inconsistent with actual life because the decision tree model places an undue emphasis on the "pay 0" variable in the data (i.e., the last repayment status). For instance, I had previously repaid and paid off the loan multiple times, but I only recently accidentally missed the due date. I am unable to benefit from the increased credit card limit in accordance with the logic of the decision tree model. There will also be others who decide to pay their bills on time for the very last time just in order to qualify for a credit card with a greater credit limit.

There is no way to take bias into account when employing a model; the findings are just a metric. A model will inevitably have bias, which could cause it to ignore any important connections between the data inputs and the predictions. The model depends heavily on the status of the immediate payment; depending on the individual's past payment behaviour, this could have a negative effect. 


