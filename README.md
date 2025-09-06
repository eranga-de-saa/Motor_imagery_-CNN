# EEG Motor Imagery Classification with CNN

A project exploring **1D Convolutional Neural Networks (CNNs)** for classifying motor imagery tasks using EEG data. The work is based on the BCI Competition IV Dataset 2a and evaluates different CNN architectures for Brain-Computer Interface (BCI) applications.

---

## Abstract

Brain-Computer Interfaces (BCIs) enable control of external devices through brain signals. Motor Imagery (MI)-based BCIs have strong potential in rehabilitation and assistive technology. EEG signals are noisy and complex, but **1D CNNs** can extract temporal patterns effectively. This project investigates three CNN architectures:

* **Shallow CNN**
* **Modified LeNet**
* **Modified AlexNet**

Results show that shallow CNNs outperform deeper networks in MI classification tasks.

---

## Dataset

* **Source**: [BCI Competition IV — Dataset 2a](http://www.bbci.de/competition/iv/)
* **Subjects**: 9 participants
* **Tasks**: 4 motor imagery tasks

  * Left hand
  * Right hand
  * Both feet
  * Tongue
* **Trials**: 288 per session (2 sessions per subject)
* **Sampling rate**: 250 Hz
* **Filtered**: 0.5–100 Hz band-pass

### Paradigm

* **t=0s**: fixation cross + warning tone
* **t=2s**: visual cue (arrow)
* **t=2–6s**: motor imagery task

---

## Preprocessing

* **Band-pass filter**: 8–30 Hz (to isolate MI-related frequencies)
* **Z-score normalization** (to normalize across participants)
* **Epoch extraction**: 3-second windows post-cue
* **Events considered**: Left hand vs. Right hand (feet & tongue excluded for consistency)

---

## Models

### 1. Shallow CNN

* 1 Conv1D layer (64 filters, kernel size=3)
* MaxPooling, Dropout
* Dense layers + Sigmoid classifier

### 2. Modified LeNet

* Based on LeNet (1998), adapted with **1D convolutions**
* 2 Conv1D layers (32, 64 filters)
* MaxPooling, Dropout
* Dense + Sigmoid output

### 3. Modified AlexNet

* Based on AlexNet (2012), adapted with **1D convolutions**
* 5 Conv1D layers (96–384 filters)
* BatchNorm, MaxPooling, Dropout
* 3 Dense layers (tanh, sigmoid output)

---

## Results

### Evaluation Method

* **Leave-One-Subject-Out Cross-Validation (LOSO-CV)**
* Ensures generalization across unseen subjects

### Accuracy (average)

| Model            | EP=100   | EP=50     | EP=25 | EP=10 |
| ---------------- | -------- | --------- | ----- | ----- |
| Shallow CNN      | 0.69     | **0.759** | 0.714 | 0.57  |
| Modified LeNet   | 0.72     | 0.732     | 0.732 | 0.65  |
| Modified AlexNet | **0.74** | 0.721     | 0.676 | 0.54  |

### AUC (at EP=50)

* **Modified LeNet**: 0.804
* **Shallow CNN**: 0.801
* **Modified AlexNet**: lower than shallow networks

### Key Takeaway

* **Shallower networks (Shallow CNN, LeNet) generalize better**
* **Deeper networks (AlexNet) risk overfitting** with limited training data

---

## Conclusion

* **1D CNNs are effective** for EEG motor imagery classification.
* Shallow CNN and Modified LeNet provide the best trade-off between accuracy and generalization.
* Future work: explore data augmentation, transformers for EEG, and subject-independent training.

---

## References

1. BCI Competition IV — Graz Data Set A (2008)
2. LeCun et al., *Gradient-Based Learning Applied to Document Recognition* (1998)
3. Krizhevsky et al., *ImageNet Classification with Deep CNNs* (2012)
4. Kiranyaz et al., *1D CNNs and Applications: A Survey* (2021)
5. Mattioli et al., *1D CNN for Motor Imagery EEG BCI* (2021)

---
