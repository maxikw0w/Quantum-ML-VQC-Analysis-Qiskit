# Quantum-ML-VQC-Analysis-Qiskit

Implementation and analysis of VQC models (Feature Maps, Ansatz, Cost Functions) in Qiskit. Applied to binary classification of medical data for diabetes diagnosis. This project serves as the foundation for my Master’s thesis research
## 🎯 Project Overview

This project focuses on the implementation and comparative analysis of Variational Quantum Classifiers (VQC) using the Qiskit framework. The primary goal was to investigate how different quantum circuit architectures and cost functions impact the training process and prediction accuracy of a binary classifier.

The model was tested on a medical dataset for diabetes diagnosis, utilizing 8 clinical parameters to predict patient health status. https://www.kaggle.com/datasets/whenamancodes/predict-diabities?resource=download
## 🔬 Methodology & Architecture

The study explored 36 different circuit configurations, evaluating three key stages of the quantum pipeline:

* **Data Encoding (Feature Maps)**: Mapping classical $\mathbb{R}^{8}$ vectors into quantum states using `RY Custom`, `ZFeatureMap`, and `ZZFeatureMap`.
* **Variational Layer (Ansatz)**: Testing various structures including `RealAmplitudes`, `Efficient SU2`, and `TwoLocal`.
* **Interpretation (Measurement)**: Comparing `Global` vs. `Local` measurement strategies.

<img width="2201" height="338" alt="obraz" src="https://github.com/user-attachments/assets/69307505-d079-44bb-8d2c-f28ce4c97d34" />

## 📊 Key Results

The research demonstrated that circuit architecture significantly influences model performance:

* **Best Configuration**: RY Custom Feature Map + Efficient SU2 Ansatz + Local Measurement.
* **Peak Accuracy**: 69.70%.
* **Observation**: The choice of cost function (MSE vs. Cross-Entropy) and data normalization to the [0, 2] range were critical for convergence.

## 💡 Discussion & Future Improvements

While the peak accuracy reached nearly 70%, there is significant room for optimization in the measurement and classical-quantum interface:

* **Current Implementation (Sampler)**: The current model utilizes the Qiskit Sampler primitive. It relies on bitstring counts to determine the probability distribution and assign classes (e.g., via the Parity function). This "counts-based" approach is sensitive to shot noise and sampling overhead.
* **Planned Upgrade (Estimator)**: To improve precision, the next iteration of this project will transition to the Qiskit Estimator primitive. Instead of processing raw bitstrings, the Estimator will calculate the expectation value of a defined observable (e.g., a Pauli-Z operator on a target qubit).
* **Expected Benefit**: Moving to expectation values via the Estimator is expected to provide smoother gradients during the optimization process, potentially leading to higher accuracy and more stable convergence of the Variational Quantum Classifier.

