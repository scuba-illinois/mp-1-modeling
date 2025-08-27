# MP1: Modeling Moderation Decisions (Due: 11:59pm on Sep 10, 2025)

This repository contains the instructions and necessary resources for the first mini-project of the semester!

### Task:

Your task is to *train a model to predict whether a comment would be removed by the moderators of its community*.

### Dataset:

For this task, you will have dataset of 106K comments consisting of 1,000 comments made in 106 Reddit communities (subreddits). Half the comments were removed by the subreddit's moderation team. 

*Content warning:* this data includes comments removed by moderators for violating subreddit rules. This may include some potentially harmful content.

#### Accessing and loading the dataset

You can access the dataset in the course Google Drive Mini Project folder [here]().

Once you've downloaded the data, use the following code snippet to load it in properly.

```python
import pandas as pd
pd.read_csv('./mp1-data.csv', index_col=0)
```

#### Columns:
* `id`: unique identifier for each comment. Make sure these do not change, they are needed to evaluate your model's accuracy.
* `body`: the body of the comment
* `subreddit`: the subreddit where the comment was originally posted
* `removed`: whether the comment was removed from the subreddit. The rows (n=26,500) with null `removed` values are the **test set**. We will evaluate your model's accuracy on the test data. 
* `context`: the text of the parent comment.

### Tips:
* Google Colab is a free resource that gives you computing resources. This includes some limited GPU access.

### What to submit:
Submit the following files to the MP-1 assignment on Canvas by 11:59 PM on Sep 10, 2025:
* *Your Python code:* you can write a Python script or do your modeling in a notebook
* *A written report:* Include a PDF file of a few paragraphs describing your approach, what other methods you tried, and the model's performance during validation. 
* *Your model's predictions:* a `predictions-[NETID].csv` file with your model's predictions ont he entire dataset. See the below section for specific details on formatting your predictions for submission.

#### Formatting the submitted predictions

You should submit predictions for the entire dataset in a file called `predictions-[NETID].csv` (replace `[NETID]` with your Illinois net ID).
* So the submitted file should contain 106,000 rows, one for each file in the original dataset
* The file should have at least the columns: `id` and `prediction`. 
* The `id` column should contain the original `id` from the dataset and the `prediction` should be the output of your model, 0 if you predict the comment wasn't removed and 1 if you predict it was.

Use the following code snippet as an example of creating properly-formatted `csv` file:
```python
df[['id','prediction']].to_csv('./predictions-[NETID].csv', quoting=csv.QUOTE_NONNUMERIC)
```
