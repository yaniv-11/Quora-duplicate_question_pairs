📝 Quora Duplicate Questions Classification
This project aims to identify duplicate question pairs from the Quora dataset. The core task is to build a machine learning model that can accurately predict whether two questions have the same intent, a classic Natural Language Processing (NLP) problem involving text preprocessing, feature engineering, and classification.

Overview
This project tackles the challenge of semantic similarity in user-generated questions. By identifying duplicate entries, platforms like Quora can enhance user experience by directing users to existing answers, thereby reducing redundancy. This notebook explores a feature-engineering-based approach to solve this classification problem.

Data Source
The dataset used is the Quora Question Pairs dataset, which contains pairs of questions along with a binary label indicating if they are duplicates.

Dataset: Quora Question Pairs

Methodology
The project follows a structured workflow, from initial data cleaning to model training and evaluation.

1. Data Cleaning and Preparation
The dataset was first loaded and prepared for analysis.

Initial Data Loading: The data was loaded from a CSV file into a pandas DataFrame.

Handling Missing Values: Rows with null values in the question1 or question2 columns were dropped to ensure data quality.

Data Sampling: A random sample of 30,000 question pairs was selected to create a manageable subset for model training.

2. Text Preprocessing
A comprehensive preprocessing pipeline was implemented to clean and normalize the question text, a crucial step for reducing noise and preparing the text for feature extraction.

Lowercasing and Stripping: All text was converted to lowercase, and leading/trailing whitespaces were removed.

Special Character Replacement:

Currency symbols ($, ₹, €) were replaced with their string equivalents ("dollar," "rupee," "euro").

The @ symbol was replaced with "at."

The dataset-specific [math] tag was removed.

Number Abbreviation: Common numerical patterns (e.g., "000" to "k," "000,000" to "m") were standardized.

Contraction Expansion: English contractions were expanded to their full forms (e.g., "don't" to "do not," "I've" to "I have").

HTML Tag and Punctuation Removal: All HTML tags and punctuation were removed, leaving only alphanumeric characters.

3. Feature Engineering
To capture the semantic similarity between question pairs, a variety of features were engineered to provide the model with a quantitative understanding of their relationship.

Basic Features
q1_len / q2_len: The character length of each question.

q1_num_words / q2_num_words: The number of words in each question.

Word-Based Features
word_common: The number of common words between the two questions.

word_total: The total number of unique words across both questions.

word_share: The ratio of common words to the total number of unique words, providing a measure of lexical overlap.

Fuzzy String Matching Features
The fuzzywuzzy library was used to generate features based on string similarity, which are robust to minor spelling differences.

fuzz_ratio: A basic measure of string similarity.

fuzz_partial_ratio: Similarity based on the best matching substring.

token_sort_ratio: Similarity after sorting the tokens in each string alphabetically.

token_set_ratio: A flexible measure that accounts for differences in word order and length.

4. Machine Learning Modeling
With the engineered features, a machine learning model was trained to perform the classification.

Model Selection: A Random Forest Classifier was chosen for its robustness and ability to handle a large number of features.

Data Splitting: The dataset was split into training and testing sets with an 80/20 ratio.

Training and Prediction: The model was trained on the training set and subsequently used to make predictions on the test set.

Results
The model's performance was evaluated using the accuracy score, which measures the proportion of correctly classified question pairs.

Accuracy: The final model achieved an accuracy of approximately 78.65% on the test set.

This result indicates that the engineered features provide a strong signal for determining question similarity. Future work could explore more advanced NLP techniques, such as word embeddings (Word2Vec, GloVe) or transformer-based models (BERT), for potential performance improvements.
