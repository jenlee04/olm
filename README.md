# olm
Simple OLM (olfaction language model) trained on SmellNet (dataset link: https://huggingface.co/datasets/DeweiFeng/smell-net/tree/main). Made for BIONB 3500 final project. 

In this model, I use a neuroscience inpsired framework (olfactory receptors -> olfactory bulb -> piriform cortex -> labeling head) and PyTorch to process odorant inputs (time series gas sensor recordings) and label them. 

Model Overview: 
- OlfactoryReceptorLayer: one feedforward linear layer that takes in a 12 dim. sensor input and outputs particular receptor activity patterns (n_receptors = 500). Frozen weights. 
- OlfactoryBulb: takes receptor activity as input for GRU, then lateral inhibition occurs over mitral cells with a learned linear projection from the receptors to mitral cells
- Piriform: uses Hebbian learning from mitral cell activity to piriform neurons in order to update weights
- Classifier head: linear softmax head that uses cross entropy loss in training for predicting odor labels from gas sensor readings

Data Usage:
All data used to train and test this model come from the SmellNet Dataset, and no PCA was carried out; only files from offline_testing, offline_training, online_nuts, and online_spices were used. 
Pre-processing -> FOTD used in order to have direct comparisons between OLM and models used in the Feng et al., 2025 paper in which this dataset was discussed. 

Training/Evaluation: 
Used both raw sensor data and FOTD pre-processed data; evaluated training loss, training accuracy, top1 accuracy, and top5 accuracy. 

Technical Blog:
<img width="812" height="171" alt="image" src="https://github.com/user-attachments/assets/561bd183-665d-450e-abf3-afc7b80a0ee1" />
<img width="406" height="194" alt="image" src="https://github.com/user-attachments/assets/a44c23a8-910f-40b3-8cde-8c9261afc8e1" />
<img width="812" height="179" alt="image" src="https://github.com/user-attachments/assets/ffb456b3-da49-44ef-8a41-bcd438e63903" />
