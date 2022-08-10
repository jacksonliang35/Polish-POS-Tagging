# Polish-POS-Tagging

## Problem Description

The problem is tagging each Polish word in a sentence with its grammatical class (POS tag) and corresponding grammatical categories (a.k.a. ctags). Up to now much work has been done One can find a clarification as well as cheatsheet [here](http://nkjp.pl/poliqarp/help/ense2.html).

## Dataset

The data comes from [the 2017 PolEval Shared Task](http://2017.poleval.pl/index.php/tasks/). We are given a set of Polish sentences as the training, validation, and test set. The lemma for each word is assumed to be known. The problem is to predict the grammatical category for each word.

## Scripts

### Baseline System for POS tagging

In the [baseline system](baseline.ipynb), bag-of-words is used as features for the classifiers, where a neighboring window of some size (i.e., a hyperparameter) with the target word at the center is used. Words are encoded using a simple counting encoder. All previously unseen feature values in the test data are casted randomly as seen feature values.

### Improved System for CTAG tagging
In the [improved system](decision_tree.ipynb), we use a set of new features: Word, Word length, Word lemma, and the last few (i.e., a hyperparameter, default 3) characters of the word. Instances are also encoded using counting encoders. All previously unseen test feature values are casted to a special tag `<UNK>` for better aggregation. There is also result analysis (including confusion matrix) at the end of the file.

### LSTM for CTAG tagging
In the [deep-learning-based system](lstm.ipynb), we investigate the performance of Polish POS tagging using LSTM models. The input list of words is connected first to an embedding layer, followed by the LSTM, whose output is mapped to the output layer for classification (i.e., applying softmax, etc.). Three different network architectures are compared:
1. simple char-level LSTM
2. char-level and lemma-level LSTM
3. char-level and lemma-level Bi-LSTM with attention
Note that the purpose of this script is not to compete with the state-of-the-art methods. Therefore, no external dictionaries (e.g., Polish word embeddings) are used, and we stop as early as 10 epochs.
