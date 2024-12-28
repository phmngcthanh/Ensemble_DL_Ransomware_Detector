# Ensemble Deep Learning Ransomware Detector
A Deep Learning ensemble that classifies Windows executable files as either benign, ransomware, or other malware.

# Setup
This project uses Python 3. For the GUI detector program `ensemblePredict.py`, the following python packages must be installed: tensorflow, keras, h5py, capstone, pefile, numpy, and scikit-learn. 

Source code for training and pre-processing for the ensemble's two models, in the folders `bin-opcodes-vec` and `bin-utf8-vec`, should run with the same pre-requisites, though `tensorflow-gpu` is recommended to acheive reasonable training times. I am not licenced to distribute the benign samples used to train the models, but these can be downloaded by installing BeautifulSoup with `pip install beautifulsoup4` and running `python benignFreewareDownloader.py`. Malware and ransomware samples were obtained from torrents available from [VirusShare.com](https://virusshare.com), after being vetted by the site's admin. 
