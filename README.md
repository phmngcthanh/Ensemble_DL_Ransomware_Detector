# Ensemble Deep Learning Ransomware Detector
A Deep Learning ensemble that classifies Windows executable files as either benign, ransomware, or other malware.

# Setup
This project uses Python 3 on Ubuntu 20.
Using 'requirements.txt' for installing enviroment.
For the GUI detector program `ensemblePredict.py`, the following python packages must be installed: tensorflow, keras, h5py, capstone, pefile, numpy, and scikit-learn. 


###
# Reproduce steps 

1. Clone this repository using 'git clone https://github.com/phmngcthanh/Ensemble_DL_Ransomware_Detector'

2. In this 'Ensemble_DL_Ransomware_Detector' directory, using 'pip install -r requirements.txt' to install required libraries.

3. Run 'python3 ensemblePredict.py' or 'python ensemblePredict.py'. An dialogue will be shown for you to select file.
