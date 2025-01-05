# Ensemble Deep Learning Ransomware Detector
A Deep Learning ensemble that classifies Windows executable files as either benign, ransomware, or other malware.

# Environment
This project uses Python 3 on Ubuntu 20.
Using 'requirements.txt' for installing enviroment


###
# Reproduce steps 

1. Clone this repository using 'git clone https://github.com/phmngcthanh/Ensemble_DL_Ransomware_Detector'

2. In this 'Ensemble_DL_Ransomware_Detector' directory, using 'pip install -r requirements.txt' to install required libraries.

3. Run 'python3 ensemblePredict.py' or 'python ensemblePredict.py'. An dialogue will be shown for you to select file.

# Ransomware Detection Models

This project uses two deep learning models to detect and classify ransomware, generic malware, and benign files. These models analyze Windows executable files in the Portable Executable (PE) format using static analysis. An ensemble combines these models to improve classification accuracy.

## Model 1: Opcode Frequency Model

### Overview

-   **Input:** The relative frequency of the top 50 opcodes in the disassembled machine code of a PE file.
-   **Architecture:** A fully connected deep neural network (DNN).
-   **Output:** Probability distribution for the three classes: benign, malware, ransomware.

### Steps

1.  **Disassembly:** The Capstone disassembly engine extracts the assembly code of the PE file.
2.  **Opcode Frequency Analysis:**
    -   The 50 most frequent opcodes are identified across the dataset.
    -   For each sample, the relative frequency of these opcodes is calculated, resulting in a 50-dimensional feature vector.
3.  **Model Structure:**
    -   5 fully connected layers with ReLU activation.
    -   Batch normalization after each layer to improve training stability.
    -   A final softmax layer outputs the probabilities for each class.

### Code Snippet



`opModel = Sequential()
opModel.add(layers.InputLayer(input_shape=(50,)))
opModel.add(layers.Dense(256, activation='relu'))
opModel.add(layers.BatchNormalization())
opModel.add(layers.Dense(128, activation='relu'))
opModel.add(layers.BatchNormalization())
opModel.add(layers.Dense(3, activation='softmax'))
opModel.compile(optimizer="rmsprop", loss='categorical_crossentropy', metrics=['accuracy'])` 



## Model 2: Greyscale Image Model (Strings as Images)

### Overview

-   **Input:** A 100x100 pixel greyscale image derived from the raw bytes of a PE file.
-   **Architecture:** A convolutional neural network (CNN).
-   **Output:** Probability distribution for the three classes: benign, malware, ransomware.

### Steps

1.  **Byte Decoding and Tokenization:**
    -   The raw bytes of the file are decoded as UTF-8 characters, forming a sequence of words.
    -   Words are tokenized and hashed into integers using feature hashing.
2.  **Image Conversion:**
    -   The integer sequence is padded or truncated to 10,000 values.
    -   Reshaped into a 100x100 grid, normalized to [0, 1], and scaled to 8-bit pixel values.
3.  **Model Structure:**
    -   Two convolutional layers with 3x3 filters, followed by batch normalization and dropout.
    -   A dense output layer applies the softmax function to classify the image.

### Code Snippet




`model = Sequential()
model.add(layers.InputLayer(input_shape=(100, 100, 1)))
model.add(layers.Conv2D(32, kernel_size=3, activation='relu'))
model.add(layers.BatchNormalization())
model.add(layers.Conv2D(16, kernel_size=3, activation='relu'))
model.add(layers.BatchNormalization())
model.add(layers.Flatten())
model.add(layers.Dense(3, activation='softmax'))
model.compile(optimizer="adamax", loss='categorical_crossentropy', metrics=['accuracy'])` 



## Ensemble Model

### Overview

The ensemble combines the predictions of both models by averaging their output probabilities. This approach boosts the overall accuracy and robustness of the classification.

### How It Works:

1.  The same PE file is pre-processed for both models.
2.  Both models generate independent predictions.
3.  The ensemble takes the average of these predictions to make the final classification.

