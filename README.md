# MP1: Modeling Moderation Decisions (Due: 11:59pm on Sep 10, 2025)

This repository contains the instructions and necessary resources for the first mini-project of the semester!

## Overview

Moderators of online communities like Reddit are often weighed down by the manual task of sifting through massive amounts of user-generated content to pick out instances of norm violations. Researchers are often trying to build tools and models that can speed up the process of removing harmful content and potentially prevent further violations. 
However, because Reddit allows its communities to institute their own rules, if you look from one community to another you might find that completely different behavior is considered norm-violating. From this flexibility comes the challenge of building helpful models of norm-violating content that can effectively assist moderators across the platform with their duties. 

With this nuance in mind, your task is to *train a model to predict whether a comment would be removed by the moderators of its community*.

## Data

Given this variability in community norms, we are providing you with a dataset consisting of comments made in 106 different Reddit communities so you can leverage those community differences. From each community, we're providing 500 removed comments and 500 non-removed comments.

*Content warning:* this data includes comments removed by moderators for violating subreddit rules. This may include some potentially harmful content.

#### Accessing and loading the dataset

You can access the dataset in the course Google Drive Mini Project folder [here](https://drive.google.com/drive/folders/1kgXkjtvMU0k9SE9R8Cui_XkELef9RMx-?usp=drive_link).

### Files

* `./mp1-data-train.csv` -- the training dataset
  * `id`: unique identifier for each comment. Make sure these do not change, they are needed to evaluate your model's accuracy.
  * `body`: the body of the comment
  * `subreddit`: the subreddit where the comment was originally posted
  * `removed`: whether the comment was removed from the subreddit. The rows (n=26,500) with null `removed` values are the **test set**. We will evaluate your model's accuracy on the test data. 
  * `context`: the text of the parent comment.
* `./mp1-data-test.csv` -- the test dataset; your objective is to predict whether these comments would be removed by the moderators of its community.

Once you've downloaded the data, you can use the following code snippet to load it in properly.

```python
import pandas as pd
train_df = pd.read_csv('./mp1-data-train.csv', index_col=0)
test_df = pd.read_csv('./mp1-data-test.csv', index_col=0)
```

### Tips:
* Google Colab is a free resource that gives you computing resources. This includes some limited GPU access.

### What to submit:
Submit the following files to the MP-1 assignment on Canvas by 11:59 PM on Sep 10, 2025:
* *Your Python code:* you can write a Python script or do your modeling in a notebook
* *A written report:* Include a PDF file of a few paragraphs describing your approach, what other methods you tried, and the model's performance during validation. 
* *Your model's predictions:* a `predictions-[NETID].csv` file with your model's predictions on the test dataset. See the below section for specific details on formatting your predictions for submission.

#### Formatting the submitted predictions

You should submit predictions for the test dataset in a file called `predictions-[NETID].csv` (replace `[NETID]` with your Illinois net ID).
* Te submitted file should contain 26,500 rows, one for each row in the test dataset
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
