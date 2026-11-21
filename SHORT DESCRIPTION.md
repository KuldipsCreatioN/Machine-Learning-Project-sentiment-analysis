Sentiment Classification of Amazon Beauty Reviews

=================================================
A controlled experimental study comparing text representations and classical classifiers for binary sentiment classification on the All Beauty category of the Amazon Reviews 2023 dataset.
Dataset Source: https://amazon-reviews-2023.github.io/

Overview & Experimental Design
------------------------------
After removing ambiguous 3-star reviews and empty entries, the dataset contains 187,132 labelled reviews (~80.7% positive, ~19.3% negative), split via an 80/20 stratified split (random_state=42) into 149,705 training and 37,427 test reviews. All vocabularies, weights, and scalers are fit strictly on the training set to prevent data leakage.

The project defines a 3x3 grid across three feature representations (20,000 top English terms, excluding stop words):
1. Bag-of-Words (BoW): Raw term frequency counts (CountVectorizer).
2. TF-IDF: Smoothed TF-IDF weights with unit L2 normalization (TfidfVectorizer).
3. TF-IDF + Numerical Features: TF-IDF combined with min-max scaled word_count, uppercase_count, exclamation_count, and question_count (20,004 features).
Each representation is paired with:
- Logistic Regression (C=1, max_iter=1000)
- Multinomial Naive Bayes (alpha=1)
- k-Nearest Neighbours (n_neighbors=5, cosine distance, brute-force)

Because positive reviews outnumber negative reviews by roughly 4.2:1, models are evaluated on accuracy, macro precision, macro recall, macro F1, and wall-clock runtime.

Current Baseline Results (Bag-of-Words)
---------------------------------------
Feature Model | Classifier          | Accuracy | Macro F1 | Time (s) | Status
--------------|---------------------|----------|----------|----------|----------
Bag of Words  | Logistic Regression | 0.9125   | 0.8495   | 9.02     | Completed
Bag of Words  | Naive Bayes         | 0.9002   | 0.8300   | 0.08     | Completed
Bag of Words  | k-NN                | -        | -        | -        | Pending


The remaining six TF-IDF and TF-IDF + numerical runs are specified in the report and evaluation loop and are currently pending execution.
