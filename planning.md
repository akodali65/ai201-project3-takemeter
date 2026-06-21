# TakeMeter Planning

## Community Choice

I chose r/nba as my online community because it has active, text-heavy discussions where people constantly share opinions about players, teams, games, trades, and coaching decisions. This community is a good fit for TakeMeter because NBA discourse varies a lot in quality: some comments are detailed basketball analysis, some are bold hot takes, and others are immediate emotional reactions.

## Label Taxonomy

### Analysis

An analysis post makes a basketball argument supported by statistics, tactical reasoning, historical comparison, or specific evidence.

Examples:
- "Denver's offense works well with Jokic because his passing creates easy shots for cutters."
- "The Celtics struggle against quick guards because their bigs often play drop coverage."

### Hot Take

A hot take expresses a strong or controversial opinion with little supporting evidence, or uses evidence mainly to push an opinion rather than build a full argument.

Examples:
- "LeBron is washed and should retire."
- "Luka is already better than prime Kobe."

### Reaction

A reaction post expresses immediate emotion, excitement, frustration, or surprise without trying to make a real argument.

Examples:
- "WHAT A SHOT!!!"
- "Fire the coach right now."

## Hard Edge Case

A difficult edge case is a post that includes one statistic but still feels like a hot take. For example: "LeBron is overrated because he is 4-6 in the Finals."

This could look like analysis because it uses a statistic, but I will label it as hot_take if the statistic is cherry-picked and the post does not explain the reasoning. If the post uses evidence to build a clear argument, I will label it as analysis.

## Data Collection Plan

I will collect at least 200 public posts or comments from r/nba. I will save them in a CSV file with columns for text, label, and notes. My target distribution is about 70 analysis examples, 65 hot_take examples, and 65 reaction examples. If one label becomes too common, I will collect more examples from the other labels so that no single label is more than 70% of the dataset.

## Evaluation Metrics

I will use overall accuracy to measure the general performance of the model. I will also use per-class precision, recall, and F1 score because this is a multi-class classification task and accuracy alone can hide problems with one specific label. I will also use a confusion matrix to see which labels the model confuses most often.

## Definition of Success

I will consider the model good enough if it reaches at least 80% accuracy on the test set and each label has an F1 score of at least 0.70. This would mean the model is not only performing well overall, but also learning each category reasonably well.

## AI Tool Plan

I plan to use AI tools in three ways. First, I will use ChatGPT for label stress-testing by asking it to generate borderline NBA posts that might be hard to label. Second, I may use an AI tool to help pre-label some examples, but I will manually review and correct every label myself. Third, after training the model, I will use AI to help identify patterns in wrong predictions, then verify those patterns myself before writing the final evaluation.