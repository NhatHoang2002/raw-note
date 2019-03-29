---
title: "IBM Data Course 3: Data Science Methodology"
categories: [data]
tags: [data, ibm data]
toc: 1
comment: 1
---

{% assign img-url = '/images/posts/data/ibm' %}

This note was first taken when I learnt the [IBM Data Professional Certificate course](https://www.coursera.org/specializations/ibm-data-science-professional-certificate) on Coursera.

<div class="see-again">
<i class="material-icons">settings_backup_restore</i>
<span markdown="1">
[Go back to Course 1 & 2](/ibm-data-professional-certificate-1).
</span>
</div>

{% include toc.html %}

## Module 1: From Problem to Approach

- Data Science Methodology aims to answer the following 10 questions in this prescribed sequence:
	- From the problem to approach:
		1. What is the problem that you are trying to solve?
		2. How can you use data to answer the question?
	- Working with the data:
		1. What data do you need to answer the question?
		2. Where is the data coming from (identify all sources) and how will you get it?
		3. Is the data that you collected representative of the problem to be solved?
		4. What additional work is required to manipulare and work with the data?
	- Deriving the answer:
		1. In what way can the data be visualized to get to the answer that is required?
		2. Does the model used really answer the initial question or does it need to be adjusted?
		3. Can you put the model into practice?

![A flowchart of Data Science Methodology]({{img-url}}/pro2app.png){:.w-700}

### Business Understanding

- If you have a deadline and a problem need to be solved. You met your boss and both of you have discussed about the track you need to keep to solve this problem. You feel that everything will be ok until you step you first steps into the solving. You realize that there are some more additional problems need to be clear but your boss is not there for your extend discussion. What will you do? Keep forward or stop and clarification? **Data Science Methodology begins with spending the time to seek clarification.**
- Clarifying the problem helps you choose the right data to be used to answer the question.
- Establishing a clearly defined question **starts with understanding the GOAL** of the person who is asking the question.
- Goal > Objectives supporting the goals
- **Case study**
	- In the case study, the question being asked is: *What is the best way to allocate the limited healthcare budget to maximize its use in providing quality care?*
	- Goals: to provide quality care without increasing costs.
	- Objectives: to review the process to identify inefficiencies.
	- **[Decision-tree model](https://www.ibm.com/support/knowledgecenter/en/SS3RA7_15.0.0/com.ibm.spss.modeler.help/nodes_treebuilding.htm)** ([wiki](https://en.wikipedia.org/wiki/Decision_tree)).
		- Decision trees are built using recursive partitioning to classify the data.
		- When partitioning the data, decision trees use the most predictive feature (ingredient in this case) to split the data.
		- Predictiveness is based on decrease in entropy - gain in information, or impurity.
	- A tree stop growing at a node when
		- Pure or nearly pure.
		- No remaining variables on which to further subset the data.
		- The tree has grown to a preselected size limit.
- **Steps**:
	1. Predict CHF readmission outcome (Y or N) for each patient
	2. Predict the readmission risk for each patient
	3. Understand explicitly what combination of events lead to the predicted outcome for each patient
	4. Easy to understand and apply to new patients to predict their readmission risk

### Analytic Approach

- Once a strong understanding of the question is established, the analytic approach can be selected. 
- This means identifying what type of patterns will be needed to address the question most effectively.
- **Types of questions?**
	- If the question is to determine probabilities of an action: use a predictive model
	- If the question is to show relationships: use a descriptive model
	- If the question requires a yes/no answer: use a classification model

### Lab: understanding problem to approach

{% include more.html content="[Go to see the notebook](https://github.com/dinhanhthi/Data_Science_Learning/tree/master/IBM%20Data%20Professional%20Certificate)." %}

## Module 1: from Requirements to Collection

### Data Requirements

- So, if the problem that needs to be resolved is the recipe, so to speak, and data is an ingredient, then the data scientist needs to identify: which ingredients are required, how to source or the collect them, how to understand or work with them, and how to prepare the data to meet the desired outcome.
- The chosen analytic approach determines the data requirements. Specifically, the analytic methods to be used require certain data content, formats and representations, guided by domain knowledge.

### Data Collection

- After the initial data collection is performed, an assessment by the data scientist takes place to determine whether or not they have what they need. As is the case when shopping for ingredients to make a meal, some ingredients might be out of season and more difficult to obtain or cost more than initially thought.
- In the initial data collection stage, data scientists identify and gather the available data resources. These can be in the form of structured, unstructured, and even semi-structured data relevant to the problem domain.

### Lab: understanding requirement to collection

{% include more.html content="[Go to see the notebook](https://github.com/dinhanhthi/Data_Science_Learning/tree/master/IBM%20Data%20Professional%20Certificate)." %}


