# TakeMeter: NBA Post Classification

## Project Overview

TakeMeter is a text classification project that categorizes posts from the NBA community into one of three labels: **analysis**, **hot_take**, and **reaction**. The goal is to compare a fine-tuned DistilBERT model with a zero-shot baseline using Groq's Llama 3.3 70B model.

---

## Community Choice

I chose the NBA community because basketball discussions naturally contain a mixture of strategic analysis, controversial opinions, and emotional reactions. These categories are common in communities such as r/nba and provide clear distinctions for a classification task.

---

## Label Definitions

### analysis

Posts that explain basketball strategy, player impact, team strengths or weaknesses, or provide reasoning and evidence.

Examples:

* "The Nuggets create efficient offense because Jokic consistently finds open teammates."
* "Boston's spacing allows Tatum and Brown to attack one-on-one effectively."

### hot_take

Strong opinions, predictions, exaggerations, or controversial statements that are subjective rather than analytical.

Examples:

* "The Lakers are guaranteed champions this season."
* "Anthony Edwards is already better than prime Harden."

### reaction

Emotional responses expressing excitement, frustration, surprise, or disappointment.

Examples:

* "WHAT A BLOCK!!!"
* "I CAN'T BELIEVE IT."

---

## Dataset

The dataset contains 200 manually labeled examples.

Label distribution:

* Analysis: 67 examples
* Hot Take: 66 examples
* Reaction: 67 examples

The dataset was created manually. AI assistance was used to generate candidate examples, but every example was reviewed and labeled by hand.

### Difficult Examples

1. **"The Celtics are overrated."**

Chosen label: hot_take

Reason: Although it references a team, it expresses an opinion without evidence.

2. **"I'm done watching this team."**

Chosen label: reaction

Reason: The statement is emotional rather than analytical.

3. **"Boston struggles because Tatum isolates too much."**

Chosen label: analysis

Reason: The statement provides an explanation and causal reasoning.

---

## Base Model and Training Setup

* Base model: `distilbert-base-uncased`
* Platform: Google Colab with a T4 GPU
* Libraries: transformers, datasets, scikit-learn

### Training Decisions

The model was trained for 3 epochs. DistilBERT was selected because it is lightweight and can be fine-tuned quickly on a free GPU. Three epochs provided enough time for learning without excessive training.

---

## Baseline Approach

The baseline used Groq's Llama 3.3 70B model with a zero-shot prompt. The prompt defined each label, provided one example for each class, and instructed the model to output only the label name.

---

## Results

| Model                       | Accuracy |
| --------------------------- | -------- |
| Groq Llama 3.3 70B Baseline | 1.000    |
| Fine-Tuned DistilBERT       | 0.467    |

---

## Per-Class Metrics (Fine-Tuned Model)

| Label    | Precision | Recall | F1   |
| -------- | --------- | ------ | ---- |
| Analysis | 0.38      | 1.00   | 0.56 |
| Hot Take | 0.00      | 0.00   | 0.00 |
| Reaction | 1.00      | 0.40   | 0.57 |

---

## Confusion Matrix

The confusion matrix is included in `confusion_matrix.png`.

The model correctly classified all analysis examples, but it consistently confused hot_take posts with analysis and also misclassified several reaction posts as analysis.

---

## Error Analysis

### Example 1

Post:

"The Lakers are guaranteed champions this season."

True label: hot_take

Predicted label: analysis

Explanation:

The model associated team-related statements with analytical language and failed to recognize unsupported predictions.

### Example 2

Post:

"I CAN'T BELIEVE IT."

True label: reaction

Predicted label: analysis

Explanation:

Short emotional posts provide little context and were often classified incorrectly.

### Example 3

Post:

"Giannis is better than Tim Duncan."

True label: hot_take

Predicted label: analysis

Explanation:

Both labels discuss players, creating vocabulary overlap that confused the model.

---

## Reflection

The fine-tuned model achieved only 46.7% accuracy, significantly below the Groq baseline. Error analysis revealed a systematic tendency to classify many posts as analysis. The model struggled to distinguish subjective opinions from evidence-based reasoning, likely because the dataset contained only 200 examples. Larger language models handled these distinctions much more effectively.

---

## AI Usage

AI tools were used in two ways:

1. ChatGPT was used to generate candidate examples for the dataset. Every example was reviewed and labeled manually.

2. ChatGPT was used to help analyze model errors and interpret the confusion matrix.

Human judgment was used to verify all labels and explanations.

---

## Spec Reflection

The project specification helped guide label design and evaluation requirements. It encouraged detailed error analysis rather than focusing only on overall accuracy.

Implementation differed from the original expectation because the fine-tuned DistilBERT model performed substantially worse than the Groq baseline. Instead of optimizing aggressively, I kept the original setup and used the resulting mistakes to perform a more thorough error analysis.

## Demo Video

Google Drive link:
https://drive.google.com/file/d/1U2QoVA8I9nxWzg15eNsGue__ePhrqmT6/view?usp=drive_link
