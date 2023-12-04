---
layout: page
title: "Deep Dive into Logistic Regression: Analyzing Handwritten Digits"
description: "A project implementing and analyzing both binary and multinomial logistic regression models to classify handwritten digits from the MNIST dataset<br><b>Using: </b><em>Logistic Regression, Python, NumPy, Matplotlib</em>"
importance: 1
category: school
---

## Project Overview

In this project, I explore the application of logistic regression in machine learning through two distinct approaches: binary logistic regression and multinomial logistic regression. The primary goal is to classify handwritten digits from the MNIST dataset, which consists of images of size 28x28 pixels in grayscale.

## Implementation Details

- <b>Languages & Libraries:</b> Python, NumPy, Matplotlib for data manipulation and visualization.
- <b>Data Preprocessing:</b> Handling grayscale image data, converting them into feature vectors.
- <b>Model Training:</b> Applying Stochastic Gradient Descent (SGD) for optimization.

## Binary Logistic Regression

- <b>Objective:</b> Classify MNIST digits into two classes using image pixels as features.
- <b>Approach:</b> Implement `model.BinaryLogisticRegressionModel` to distinguish between two specific digit classes (e.g., "7" vs. "9"), represented as "0" and "1".
- <b>Analysis:</b> Generate and analyze accuracy curves, confusion matrix, model weights, and specific erroneous predictions to understand the model's performance and limitations.

### Insights and Analysis

#### Accuracy Curves

<div class="row">
    <!-- First Image -->
    <div class="col-md-6 mt-3">
        {% include figure.html path="assets/img/binary-train-accuracy-curve.png" title="Train accuracy curve" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
            Train accuracy curve.
        </div>
    </div>

    <!-- Second Image -->
    <div class="col-md-6 mt-3">
        {% include figure.html path="assets/img/binary-test-accuracy-curve.png" title="Test accuracy curve" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
            Test accuracy curve.
        </div>
    </div>
</div>

#### Confusion Matrix

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/binary-confusion-matrix.png" title="Confusion Matrix" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Accuracy: 93.9617% (1914 out of 2037)

Confusion Matrix:
<table>
    <tr>
        <th></th>
        <th>7</th>
        <th>9</th>
    </tr>
    <tr>
        <th>7</th>
        <td>946</td>
        <td>82</td>
    </tr>
    <tr>
        <th>9</th>
        <td>41</td>
        <td>968</td>
    </tr>
</table>

#### Non-Bias Term Weights

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/binary-non-bias-term-weights.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

- The color bar on the right indicates the scale of the weights. In this heatmap, colors closer to the top of the color bar (yellows and greens) represent higher weights, while colors towards the bottom (blues and purples) represent lower weights. Yellow indicates strong positive weights, and purple indicates strong negative weights.
- <b>Positive Weights (Yellow):</b> These areas are where the pixel values significantly contribute to the model predicting the digit as a 7. It means that for pixels in these regions, the presence of a certain intensity (white since it's a typical black-on-white handwriting dataset) will push the model towards identifying a 7.
- <b>Negative Weights (Purple):</b> These areas are where the pixel values contribute to the model predicting the digit as a 9. It implies that for these pixels, a certain intensity (black) will push the model towards identifying a 9.
- <b>Neutral Weights (Green/Blue):</b> These pixels don't have much influence on the differentiation between 7 and 9, meaning that their values do not significantly sway the model towards either digit.
- The model uses these weights to decide whether a new, unseen image of a digit is more likely to be a 7 or a 9. When it 'sees' an image, it will multiply the pixel values by these weights to reach a decision.

#### Analysis of Erroneous Predictions

<table>
    <tr>
        <td>{% include figure.html path="assets/img/error1.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error2.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error3.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error4.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error5.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
    </tr>
    <tr>
        <td>{% include figure.html path="assets/img/error6.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error7.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error8.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error9.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
        <td>{% include figure.html path="assets/img/error10.png" title="Non-Bias Term Weights" class="img-fluid rounded z-depth-1" %}</td>
    </tr>
</table>

Some potential reasons why the model made errors on these cases/what it failed to capture:
- Ambiguity in Digit Formation: If the shapes are not clearly defined or have ambiguous features that could belong to multiple digits, the model might be confused. For example, if a '9' is written with a very small loop, it might resemble a '7'.
- Noise and Distortions: Variability in writing style, such as slants, loops, or breaks in the strokes, can introduce noise that the model fails to handle well.
- Model's Feature Sensitivity: The model may not be sensitive to certain features that differentiate the digits. For example, the intersection in the '7' or the loop in the '9'.

Additional features that may help the model make correct predictions on these error cases:
- Contextual Features: Incorporating context, like the relative position of loops and lines, could help distinguish between similar digits.
- Stroke Analysis: Analyzing the order and direction of strokes could provide more insight into the intended digit.
- Structural Decomposition: Breaking down the digit into constituent parts and analyzing the presence or absence of these parts (like the crossbar in a '7' or the loop in a '9').
- Convolutional Features: Using Convolutional Neural Networks (CNNs) to capture spatial hierarchies in the data that simple weight matrices might miss.
- Data Augmentation: Increasing the diversity of the training data by introducing variations in digit representation, such as rotations, scaling, and noise.
- Complexity Control: Applying regularization techniques to prevent overfitting to the training data.
- Error Analysis: Conducting a thorough error analysis to understand the specific cases where the model fails and adapting the training strategy accordingly.
- Ensemble Methods: Using ensemble methods that combine the predictions of multiple models to improve accuracy.
- Human-like Feature Extraction: Incorporating features that mimic human visual perception, such as recognizing overall shape patterns before focusing on details.

## Multinomial Logistic Regression

- <b>Objective:</b> Extend classification to all 10 digit classes in the MNIST dataset.
- <b>Approach:</b> Utilize `model.MultiLogisticRegressionModel` for a more comprehensive classification covering all digits from “0” to “9”.
- <b>Analysis:</b> Similar to the binary case, this section involves plotting training and test accuracy curves, confusion matrices, and an examination of the learned weights for all digit classes.
- <b>Performance Optimization:</b> Due to the larger scale of data (60K training images and 10K test images), strategies such as training on a fraction of the data and using fewer iterations during development and debugging are employed for efficient performance without compromising accuracy​.