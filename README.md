# CapstoneDesignCourse

This repository is for code for the Capstone Design Course (CSC490) on medical image datasets.

# Introduction
The focus of the project was to improve on past deep learning approaches to generate polyp segmentation. The decided approach was to merge two different ideas from two papers. Tajbakhsh et al.[2] uses shape and context information to improve models. We decided to introduce a fourth channel to a bronchial segmentation transformer net called ESFPNet[1] to provide it with such shape information and check if it improves performance on polyp segmentation. Besides combining the two ideas, we merged 3 different datasets to increase the number of data inputs to try to make the model more robust and more applicable to real world situations. It is also important to note that  the edge is used as a high level heuristic as Transformers learn a lot of low level features.

# Data
We decided to merge three different datasets in order to increase the amount of data to train the model, since there is not a lot of polyp data available. The three chosen datasets are: **ETIS-Larib, CVC-Colon DB, and Kvasir Seg.**
The combined dataset has a total of 1381 images, where 1104 is used for training and 277 for testing.

Initial image resolution:
- Kvasir Seg: 616x528
- Etis-Larib: 1225x966
- CVC-ColonDB: 574x500
Resolution for training: 352x352

# Results
|Approach|Final validation coeff.|mdice score|
|:------:|:---------------------:|:---------:|
|Only Etis Larib(200 epoch pretrained weights + 150 epochs)|0.854|0.887|
|Combined Dataset (200 epoch pretrained weights + 150 epochs)|0.953|0.957|
|Combined Dataset with edge channel (150 epochs)|0.775|0.775| 

# Data Loading Instructions
Add the following directory to your Google Drive under "MyDrive":  https://drive.google.com/drive/folders/1VHw4MLp4KkUQaps07oi3GQAD9YY5kqtf?usp=sharing
This should give you access to our combined datasets, edge datasets and modified model.

# Training Instructions
NOTE: CUDA supported GPU is required for training. We used GPUs provided by Google Colab for this. 
Clicking on "Run All" in the Polyp_ESFPNet.ipynb notebook will begin training on our 4 channel dataset and modified ESFPNet model. Follow the instructions given by the "INSTR" comments across the notebook if you want to train on different data, number of channels or model architecture. (Ctrl+F "INSTR" to find instructions across the notebook). If you convert one part of the code to run on 3 channel images, you will have to change all the code instances marked by "INSTR" to its 3 channel version and vice-versa. <br /> <br />
Ensure that you have the data from our shared gdrive under your "MyDrive" directory before training. <br /> <br />
If you would like to extract edge layers on data, run edge_detection_script.ipynb and convert_npy_png.ipynb. However this should be required only if you are creating a new dataset as the all the edge layers are available on the shared gdrive for our Cobined dataset and their individual sub-datasets. 

# References
Our code is a modification of the code for ESFPNet provided here: https://github.com/dumyCq/ESFPNet 
For the edge_detection_script, the source code is from: https://github.com/acarcher/hed-opencv-dl
<br />
[1] Chang, Qi, et al. "ESFPNet: efficient deep learning architecture for real-time lesion segmentation in autofluorescence bronchoscopic video." arXiv preprint arXiv:2207.07759 (2022). <br />
[2] Tajbakhsh, Nima, Suryakanth R. Gurudu, and Jianming Liang. "Automated polyp detection in colonoscopy videos using shape and context information." IEEE transactions on medical imaging 35.2 (2015): 630-644. <br />
[3] Silva, Juan, et al. "Toward embedded detection of polyps in wce images for early diagnosis of colorectal cancer." International journal of computer assisted radiology and surgery 9.2 (2014): 283-293. <br />
[4] Xie, Saining, and Zhuowen Tu. "Holistically-nested edge detection." Proceedings of the IEEE international conference on computer vision. 2015 <br />
