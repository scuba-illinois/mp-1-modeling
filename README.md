# MP-1: Modeling Moderation Decisions (Due: 11:59pm on Sep 10, 2025)

This repository contains the instructions and necessary resources for the first mini-project of the semester!

## Overview

Moderators of online communities like Reddit are often weighed down by the manual task of sifting through massive amounts of user-generated content to pick out instances of norm violations. Researchers are often trying to build tools and models that can help triage harmful content for moderators and potentially prevent further violations. 
However, because Reddit allows its communities to institute their own rules, if you look from one community to another you might find that completely different behavior is considered norm-violating. From this flexibility comes the challenge of building helpful models of norm-violating content that can effectively assist moderators across the platform with their duties. 

## Learning Objectives

By the end of this MP, you will be able to:

* Work with the `pandas` Python library
* Use Python packages to train a prediction model with cross validation
* Describe your model performance and synthesize insights
  

## Your Tasks

For this MP, you have two tasks:

**Task 1:** *train ML models to predict whether a comment would be removed by the moderators of its community*. As indicated in the grading section (see end of this document), use cross validation and report the model performance.

**Task 2:** *train a global Science model and 3 individual community models for r/science, r/Futurology, and r/askscience.*

## Data

Given this variability in community norms, we are providing you with a dataset consisting of comments made in 106 different Reddit communities so you can leverage those community differences. From each community, we're providing 500 removed comments and 500 non-removed comments.

*Content warning:* this data includes comments removed by moderators for violating subreddit rules. This may include some potentially harmful content.

#### Accessing and loading the dataset

You can access the dataset in the course Google Drive Mini Project folder [here](https://drive.google.com/drive/folders/1kgXkjtvMU0k9SE9R8Cui_XkELef9RMx-?usp=drive_link).

Enable Google Apps @ Illinois [here](https://cloud-dashboard.illinois.edu/) before being able to access Google Drive files using your Illinois account! 

### Files

* `./mp1-data-train.csv` -- the training dataset
  * `id`: unique identifier for each comment. Make sure these do not change, they are needed to evaluate your model's accuracy.
  * `body`: the body of the comment
  * `subreddit`: the subreddit where the comment was originally posted
  * `removed`: whether the comment was removed from the subreddit (0 if comment was not removed, 1 if comment is removed). The rows (n=26,500) with null `removed` values are the **test set**. We will evaluate your model's accuracy on the test data. 
  * `context`: the text of the parent comment.
* `./mp1-data-test.csv` -- the test dataset; your objective is to predict whether these comments would be removed by the moderators of its community.
* `./mp1-task-2-holdout.csv` -- the holdout set for task 2. You should use this data to evaluate your global and subreddit-specific models trained for task 2.

Once you've downloaded the data, you can use the following code snippet to load it in properly.

```python
import pandas as pd
train_df = pd.read_csv('./mp1-data-train.csv', index_col=0)
test_df = pd.read_csv('./mp1-data-test.csv', index_col=0)
task2_holdout = pd.read_csv('./mp1-task-2-holdout.csv', index_col=0)
```

### Tips:
* Google Colab is a free resource that gives you computing resources. This includes some limited GPU access.
* Here are some potentially useful resources to get you started with your modeling setup:
   * Using BERT:
      * [Conversations Gone Alright: Quantifying and Predicting
Prosocial Outcomes in Online Conversations](https://drive.google.com/file/d/1-DGqgtXOBt3u_yVzM5YovLECZur4GqzN/view)
      * [Venire: A Machine Learning-Guided Panel Review System for
Community Content Moderation](https://arxiv.org/pdf/2410.23448)
   * Using Sklearn:
      * [Conversational Resilience: Quantifying and Predicting Conversational Outcomes Following Adverse Events](https://ojs.aaai.org/index.php/ICWSM/article/view/19314) 
      * [The Bag of Communities: Identifying Abusive Behavior Online with Preexisting Internet Data](https://dl.acm.org/doi/abs/10.1145/3025453.3026018)
   * Using LLMs:
      * [MoMoE: Mixture of Moderation Experts Framework
for AI-Assisted Online Governance](https://arxiv.org/pdf/2505.14483)

## What to submit:
Submit the following files to the MP-1 assignment on Canvas by 11:59 PM on Sep 10, 2025:
* *Your Python code:* you can write a Python script or do your modeling in a notebook
* *Your model's predictions for task 1:* a `predictions-[NETID].csv` file with your model's predictions on the test dataset. See the next section for specific details on formatting your predictions for submission.
* *A written report for both tasks:* Using [this](https://docs.google.com/document/d/1zBLe6tQo1JXezl5mzyuEwdaBCpqtMOhZ9N4rQ1z_MLk/edit?usp=drive_link) template, include a PDF file of a few paragraphs describing your approach for each task, what methods you tried, and the model's performance on a holdout set.
    * For task 2, include the following table reporting how each model performs on each subreddit's data on a holdout set. Compare the performance of the global model vs. the subreddit-specific models.

 | Subreddit | Accuracy of Global Model | Accuracy of r/science Model | Accuracy of r/Futurology Model | Accuracy of r/askscience Model|
| ---- | ---- | ---- | ---- | ---- |
| r/science
| r/Futurology
| r/askscience


#### Formatting the submitted predictions

You should submit predictions for the test dataset in a file called `predictions-[NETID].csv` (replace `[NETID]` with your Illinois net ID).
* The submitted file should contain 26,500 rows, one for each row in the test dataset
* The file should have only two columns: `id` and `prediction`. 
* The `id` column should contain the original `id` from the dataset and the `prediction` should be the output of your model, 0 if you predict the comment wasn't removed and 1 if you predict it was.

Use the following code snippet as an example of creating properly-formatted `csv` file:
```python
test_df[['id','prediction']].to_csv('./predictions-[NETID].csv', quoting=csv.QUOTE_NONNUMERIC)
```

#### Sample submission file

Your submitted predictions `csv` should look like this:

```csv
id,prediction
1,1
2,0
3,0
...
```

## Grading

You will be evaluated on the tasks as follows:

**Task 1:**
* (2 points) Report template is completed.
* (1 points) Having a reasonable model architecture implemented in code
* (1 point) Cross validation performance as reported in the written report.
* (1 point) Performance on test set

**Task 2:**
* (2 points) Report template is completed.
* (2 points) Having a reasonable model architecture implemented in code
    * (1 point) Global model is implemented
    * (1 point) Subreddit-specific models are implemented
* (1 point) Holdout set performance as reported in the written report.

