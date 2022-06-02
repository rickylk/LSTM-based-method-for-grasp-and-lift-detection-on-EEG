![capture_001_02062022_01551122](https://user-images.githubusercontent.com/21188544/171472880-b9909c94-5293-477d-9443-7f5620cfcaa2.jpg)

# Final Project
## Grasp-and-Lift-Detection-on-EEG
This is project for fulfilment of the course Brain Computer Interfaces and Application. <br />
National Tsing Hua University, Taiwan, R.O.C, Spring Semester 2021. <br /> <br />

### Introduction
![capture_001_02062022_030150](https://user-images.githubusercontent.com/21188544/171482094-eae8c6ea-ebeb-4df1-8442-c8b805d3283a.jpg)
After the first EEG data was record in 1924 by Hans Berger, a German psychiatrist. There are many researches developed based on EEG data, since EEG data is rich in infortaion and containing all body activities in term of signal. BCI is also one popular research domain that mainly developed based on EEG data with an intention to help people to be able to directly control the computer from the brain. Especially, for people with disabilities, BCI helps to enhance their life quality to live more independently and more convenient.<br />

In this project, we implement and develop the machine learning approach to classify the different hand movements using EEG data.<br />
This challenge was a research prediction competition on Kaggle in 2015. <br />
Please find more information about the competition [here ](https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data)


### Project objective:
1. To find the significant features that can improve the model performance.
2. To implement the classification model to accurately classify the different hand movements by using EEG signals.
3. To find the high heavyweight channels, cancel other channels to increase the efficiency of the model.<br />
 
### Dataset:
We use 'Grasp-and-Lift EEG Detection (GAL) dataset' (Luciw, Jarocka & Edin, 2014) as our dataset. <br />
The dataset is available on Kaggle and was used for a prediction competition in 2015. <br />
This dataset records both EEG data, EMG data and 3D position of hands and object. However, we will focus on EEG data only for this study. <br /> 
The brief information of the dataset is shown below; <br />
  - Using EEG sensor ActiCap 32 channals 
  - 12 participants, 10 series of trial subjects, approximately 30 trials on each series, in total 3,960 trials are recorded.
  - Object used and action:
          - different weight (165, 330, 660 g).
          - different surface (sandpaper, suede, silk surface).
          - different action e.g. enforcing change in fingertip, grasp with thumb and index finger and  lift and hold .
  - 6 labels: hand start, first digit touch, both start load phase, lift off, replace and both released.
  - 
Please find the dataset in [folder data](https://github.com/rickylk/LSTM-based-method-for-grasp-and-lift-detection-on-EEG/tree/main/data) or [click]( https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data) <br />
For more information on how the data was recored, please refer to [click](https://www.nature.com/articles/sdata201447) <br />

### <s> Methodology:</s> 
Thi

###  <s>Result:</s>
###  <s>Demo:</s>

### Acknowledgements:
- Luciw, M. D., Jarocka, E., & Edin, B. B. (2014). Multi-channel EEG recordings during 3,936 grasp and lift trials with varying weight and friction. Scientific data, 1(1), 1-11. ([PDF](https://www.nature.com/articles/sdata201447))


----------------------------------------------------------------------------
#### Author.
Pattamon Rattanapan  ID 108065436, 林孟萱 ID 110065509, 吳余山 ID 110033408  



