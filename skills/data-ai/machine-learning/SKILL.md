---
name: machine-learning
description: Machine learning, deep learning, neural networks, and AI systems. Master algorithms, model training, and production ML systems.
---

# Machine Learning & AI

## Quick Start

Machine learning enables systems to learn from data and make predictions:

```python
# Scikit-learn Classification
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
```

## Deep Learning

```python
# TensorFlow/Keras Neural Network
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(128, activation='relu', input_shape=(784,)),
    keras.layers.Dropout(0.2),
    keras.layers.Dense(64, activation='relu'),
    keras.layers.Dense(10, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

model.fit(X_train, y_train, epochs=10, batch_size=32, validation_split=0.1)
```

## NLP & Transformers

```python
from transformers import pipeline

# Text Classification
classifier = pipeline("sentiment-analysis")
result = classifier("This movie is amazing!")

# Named Entity Recognition
ner = pipeline("ner")
tokens = ner("John Smith works at OpenAI")

# Text Generation
generator = pipeline("text-generation", model="gpt2")
text = generator("The future of AI is", max_length=50)
```

## Core Concepts

- **Supervised Learning** - Learning with labeled data
- **Unsupervised Learning** - Finding patterns in unlabeled data
- **Reinforcement Learning** - Learning through rewards/penalties
- **Feature Engineering** - Creating relevant input features
- **Model Evaluation** - Accuracy, precision, recall, F1-score
- **Overfitting** - Model memorizes training data
- **Cross-validation** - Testing on different data splits

## Best Practices

- Collect quality training data
- Split data: training (70%), validation (15%), testing (15%)
- Start simple, increase complexity gradually
- Monitor for overfitting
- Use appropriate metrics for your problem
- Document your experiments
- Version your models
- Test on new data

## Resources

- [Scikit-learn Docs](https://scikit-learn.org)
- [TensorFlow Docs](https://tensorflow.org)
- [Hugging Face](https://huggingface.co)
- [Fast.ai](https://fast.ai)
