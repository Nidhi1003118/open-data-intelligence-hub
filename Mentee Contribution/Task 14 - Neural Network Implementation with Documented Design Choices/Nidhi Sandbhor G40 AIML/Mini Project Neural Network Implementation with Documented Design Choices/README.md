# Casting Defect Detection using CNN

## Project Overview

This project develops a Convolutional Neural Network (CNN) for automated
classification of casting products into two categories:

- **Non-defective**
- **Defective**

The project demonstrates how deep learning can be used as a decision-support
system for industrial quality inspection.

---

## Dataset

The original dataset contains two classes:

- `ok_front` – non-defective casting images
- `def_front` – defective casting images

The dataset was split into:

- **70% Training**
- **15% Validation**
- **15% Testing**

The test images were kept separate from training so that the final model
could be evaluated on unseen data.

---

## Technologies Used

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- VS Code

---

## Project Workflow

1. Load the casting image dataset
2. Organize images into training, validation and test sets
3. Resize images to `224 × 224`
4. Apply data augmentation
5. Build a CNN model
6. Compile the model
7. Train using Early Stopping
8. Plot training and validation accuracy/loss
9. Evaluate the model on the test dataset
10. Generate classification report
11. Generate confusion matrix
12. Test unseen images
13. Produce a quality-control recommendation

---

## Data Augmentation

The following augmentation techniques were used:

- Horizontal Flip
- Rotation
- Zoom
- Translation
- Contrast Adjustment

Data augmentation helps the model become more robust to variations in
casting images.

---

## CNN Architecture

The model uses the following structure:

- Input: `224 × 224 × 3`
- Data Augmentation
- Rescaling
- Conv2D: `32 filters`
- MaxPooling
- Conv2D: `64 filters`
- MaxPooling
- Conv2D: `128 filters`
- MaxPooling
- Global Average Pooling
- Dropout: `0.40`
- Dense: `64 neurons`
- Dropout: `0.30`
- Output: `1 neuron with Sigmoid activation`

---

## Design Decisions

| Design Choice | Selected Value | Reason |
|---|---|---|
| Image Size | 224 × 224 | Balances image detail and computational cost |
| Problem Type | Binary Classification | Two classes: defective and non-defective |
| Model Type | CNN | Suitable for image classification |
| Convolution Filters | 32, 64, 128 | Learns increasingly complex image features |
| Kernel Size | 3 × 3 | Effective for local feature extraction |
| Hidden Activation | ReLU | Efficient and commonly used in CNNs |
| Pooling | MaxPooling | Reduces feature dimensions and computation |
| Output Activation | Sigmoid | Produces probability for binary classification |
| Optimizer | Adam | Adaptive and beginner-friendly optimizer |
| Learning Rate | 0.001 | Reasonable starting value for Adam |
| Loss Function | Binary Cross-Entropy | Suitable for binary classification |
| Batch Size | 32 | Good balance between memory and training |
| Maximum Epochs | 25 | Allows sufficient training with Early Stopping |
| Dropout | 0.40 | Helps reduce overfitting |
| Data Augmentation | Flip, Rotation, Zoom, Translation, Contrast | Improves robustness |
| Evaluation Metrics | Accuracy, Precision, Recall | Measures overall and defect performance |

---

## Model Compilation

The model was compiled using:

- **Optimizer:** Adam
- **Learning Rate:** 0.001
- **Loss:** Binary Cross-Entropy
- **Metrics:** Accuracy, Precision and Recall

---

## Training

The model was allowed to train for a maximum of **25 epochs**.

Early Stopping was used to stop training when validation loss stopped
improving.

The training completed after **12 epochs**, helping avoid unnecessary training
and potential overfitting.

---

## Training and Validation Analysis

The training and validation accuracy and loss were plotted to analyze model
learning behaviour.

### Observations

- Training accuracy improved during training.
- Training accuracy reached approximately **69.20%**.
- Best validation accuracy was approximately **62.05%**.
- Best validation loss was approximately **0.6155**.
- The difference between training and validation performance indicates some
  signs of overfitting.
- Early Stopping helped prevent unnecessary additional training.

---

## Final Model Performance

| Metric | Result |
|---|---:|
| Test Accuracy | **62.24%** |
| Test Precision | **61.46%** |
| Test Recall | **100%** |
| Test Loss | **0.6035** |
| Best Validation Accuracy | **62.05%** |
| Training Epochs Completed | **12 / 25** |

### Performance Interpretation

The model achieved a test accuracy of approximately **62.24%**.

The test recall for the defective class was **100%**. This is important in
quality control because missing a defective product may allow it to pass
inspection and reach the customer.

The precision was approximately **61.46%**, indicating that some products
classified as defective may actually be non-defective.

---

## Why Recall for the Defective Class Matters

Recall is especially important for the defective class because a false negative
means that a defective product is incorrectly classified as non-defective.

In a quality-control system, this can be risky because the defective product
may pass inspection and reach the customer.

Therefore, high recall for the defective class helps ensure that most defective
products are detected and sent for manual inspection.

In this project, the test recall was **100%**, meaning all defective samples in
the test dataset were detected by the model.

---

## Confusion Matrix

A confusion matrix was generated to analyze:

- True Negative
- False Positive
- False Negative
- True Positive

False negatives are particularly important because they represent defective
products incorrectly classified as non-defective.

---

## Unseen Test Image Prediction

Five unseen images from the test dataset were selected for individual
prediction.

For each image, the model provides:

- Prediction
- Defect Probability
- Recommended Action

### Decision Rule

- **Probability ≥ 50%** → **Defective** → Send for manual inspection
- **Probability < 50%** → **Non-defective** → Product may proceed

This demonstrates how the CNN can be integrated into a quality-control
decision-support workflow.

---

## Sample Predictions

### Non-defective Example

- Prediction: **Non-defective**
- Defect Probability: **39.46%**
- Recommended Action: **Product may proceed**

### Defective Example

- Prediction: **Defective**
- Defect Probability: **93.46%**
- Recommended Action: **Send for manual inspection**

---

## Project Conclusion

The CNN model was developed to classify casting products into defective and
non-defective categories.

The model achieved a test accuracy of approximately **62.24%**, with a
precision of **61.46%** and recall of **100%** for the defective class.

The high recall is important for a quality-control application because
defective products should not be incorrectly passed as non-defective.

The project demonstrates the use of deep learning for automated casting defect
detection and can be used as a decision-support system for industrial quality
inspection.

Further improvements could be achieved using a larger dataset, more advanced
CNN architectures and additional hyperparameter tuning.

---

## Future Improvements

- Use transfer learning with architectures such as MobileNet or ResNet
- Increase the size and diversity of the dataset
- Tune the classification threshold
- Perform additional hyperparameter optimization
- Improve the model's overall accuracy and precision
- Deploy the model as a web-based quality inspection application

---

## Project Structure

```text
Casting-Defect-Detection/
│
├── casting_defect_detection.ipynb
├── README.md
├── casting_split/
│   ├── train/
│   ├── validation/
│   └── test/
└── best_casting_defect_model.keras