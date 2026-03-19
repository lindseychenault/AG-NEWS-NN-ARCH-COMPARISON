# AG News Neural Network Architecture Comparison

## Overview

This project evaluates how neural network architecture impacts performance in multiclass text classification using the AG News dataset. The study isolates architecture as the primary variable by holding all core training conditions constant across experiments.

Fifteen models were implemented and compared, including dense, recurrent, and convolutional architectures. The goal is to determine whether increasing model complexity leads to better generalization in short-form text classification.

## Dataset

* **Source:** AG News (TensorFlow Datasets)
* **Classes:** World, Sports, Business, Science/Technology
* **Samples per class:** 31,900
* **Total samples:** ~127,600
* **Median length:** ~20 tokens
* **Max length:** 95 tokens

The dataset is balanced and consists of short, information-dense news summaries, making it well-suited for controlled architectural comparisons.

## Objective

Does increasing neural network complexity improve generalization performance when classifying short-form text under identical training conditions?

## Experimental Design

All models were trained under the same setup to ensure fair comparison:

* Sequence length: 128 tokens
* Embedding dimension: 256
* Batch size: 100
* Optimizer: RMSprop
* Loss: Sparse categorical crossentropy
* Epochs: up to 10 (early stopping applied)

The TextVectorization layer was fit only on training data to prevent data leakage.

## Models Evaluated

* Dense (baseline)
* SimpleRNN (multiple configurations)
* Bidirectional RNN
* LSTM (single-layer, stacked, bidirectional)
* 1D CNN (multiple configurations)

## Preprocessing Experiments

* Vocabulary sizes: 1,000 / 5,000 / 20,000
* Stopword removal vs. full vocabulary
* Default vs. fixed-length sequence encoding

## Key Results

### Best Performing Model

* **Dense Neural Network**

  * Test Accuracy: **0.895**
  * Test Loss: 0.309
  * Training Time: ~354 seconds

### Model Comparisons

* **SimpleRNN**

  * Accuracy: 0.880–0.891
  * Much higher training time (>1000s)
* **LSTM**

  * Accuracy: 0.860–0.865
  * Significantly slower (up to 4300s)
* **CNN**

  * Accuracy: 0.850–0.852
  * Moderate training cost

### Key Insight

In short-text classification, **lexical signals dominate**, making complex sequence modeling unnecessary.

## Conclusions

* Increased architectural complexity did **not** improve performance.
* Dense models achieved the best balance of:

  * Accuracy
  * Training efficiency
  * Generalization
* Sequential and convolutional models added computational cost without meaningful gains.

## Takeaways

* Model complexity should match data characteristics.
* Short, structured text benefits from simpler architectures.
* More parameters and memory mechanisms do not guarantee better results.
* Efficient models are often more practical for production systems.

## Applications

* News classification
* Content tagging
* Customer support routing
* Intent classification
* Real-time NLP systems

## Tech Stack

* Python
* TensorFlow / Keras
* NumPy / Pandas
* Matplotlib / Seaborn

## Future Work

* Test transformer-based models (e.g., BERT)
* Evaluate performance on longer-form text datasets
* Explore hybrid architectures (CNN + LSTM)
* Hyperparameter tuning for each architecture individually

## Author

Lindsey Chenault
MSDS 458 – Third Programming Assignment
February 2026
