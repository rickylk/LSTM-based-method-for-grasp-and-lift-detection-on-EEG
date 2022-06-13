![capture_001_02062022_01551122](https://user-images.githubusercontent.com/21188544/171472880-b9909c94-5293-477d-9443-7f5620cfcaa2.jpg)

# Final Project
## Grasp-and-Lift-Detection-on-EEG
This is project for fulfilment of the course Brain Computer Interfaces and Application. <br />
National Tsing Hua University, Taiwan, R.O.C, Spring Semester 2021. <br /> <br />

### Introduction
![capture_001_02062022_030150](https://user-images.githubusercontent.com/21188544/171482094-eae8c6ea-ebeb-4df1-8442-c8b805d3283a.jpg)
After the first EEG data was record in 1924 by Hans Berger, a German psychiatrist. There are many researches developed based on EEG data, since EEG data is rich in infortaion and containing all body activities in term of signal. BCI is also one popular research domain that mainly developed based on EEG data with an intention to help people to be able to directly control the computer from the brain. Especially, for people with disabilities, BCI helps to enhance their life quality to live more independently and more convenient.<br />

In this project, we implement and develop the machine learning approach to classify the different hand movements using EEG data.<br />
This challenge was a research prediction competition on Kaggle in 2015, which the competition result can be found [here ](https://hal.archives-ouvertes.fr/hal-01349562/)<br />
For more information about the competition, [Pleas click here ](https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data)


### Project objective:
1. To find the significant features that can improve the model performance.
2. To implement the classification model to accurately classify the different hand movements by using EEG signals.
3. To find the high heavyweight channels, cancel other channels to increase the efficiency of the model.<br />
 

### Dataset:
We use 'Grasp-and-Lift EEG Detection (GAL) dataset' (Luciw, Jarocka & Edin, 2014) as our dataset. <br />
The paper was published in 2014 and the dataset was used for a prediction competition on Kaggle in 2015. <br />

Apart from the competition, this data is also used for many studies for example to compare the performance of algorithm  
to detect hand movement from EEG data (Várszegi, K., 2016), to improve the classification method on EEG data using 
feature priority based analysis and CNN in 2019 (Li et al., 2019),and to forecast Grasp-and-Lift Movement (Gordienko et al., 2021), 

This dataset not contains only EEG data but also includes EMG data and 3D of both hand and object position.  <br />
However, in this study, we will focus on EEG data only. The brief information of the dataset is shown below; <br />
  - 12 participants, 10 series of trial subjects and ~ 30 trials on each series, 3,960 trials in total.<br />
  - 6 labels: Hand Start, First Digit Touch, Both Start Load Phase, Lift Off, Replace, Both Released.
  - Object used and action:<br />
        - different weight (165, 330, 660 g).<br />
        - different surface (sandpaper, suede, silk surface).<br />
        - different action e.g. enforcing change in fingertip, grasp with thumb and index finger and  lift and hold.<br />
For data collection, this dataset is recorded using EEG sensor ActiCap 32 channals in conjunction with BrainAmp EEG signal amplifier. After preprocessing, the ready to use data sample rate is 500 Hz.
        
![capture_001_13062022_014953](https://user-images.githubusercontent.com/21188544/173246397-fa775461-8c87-4b51-9361-91c28a9a5603.jpg)
Figure1 displays the EEG map of ActiCap and the location of each channel. For our task, we are going to classify the different hand movement which is controlled by primory motor cortex and primary sensory cortex, figure 2. So, we will focus on using the data which location is on these part of the brain which are: T7, C5, C3, C1, Cz, C2, C4, C8, T8, TP9, TP7, CP5, CP1, CPz, CP2, CP4, Cp6, TP8 and TP10.

To download the file, please visit [folder data](https://github.com/rickylk/LSTM-based-method-for-grasp-and-lift-detection-on-EEG/tree/main/data) or [click]( https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data) <br />
For more information about the dataset collection methodology, please refer to [click](https://www.nature.com/articles/sdata201447) <br />

### Methodology: 

#### Data Preprocessing:
![capture_006_13062022_223220](https://user-images.githubusercontent.com/21188544/173377539-f0caa1d4-efcb-4f1e-a294-2d9b736a7fb4.jpg)
From figure 3, we visualize the raw data using EEGlab. We can see that the raw data contains a lot of artifacts for example the eye blinking that clearly display in channel 1,2,3 and 4. To remove these artifacts will help to improve the quality of our data before feeding them to the next process of feature extraction and classification. We apply multiple method of preprocessing as following;
- Preprocessing<br />
   -  Bandpass filter <br />     
   -  Bandpass-Beta filter   <br />     
   -  FFT<br />
   -  Standardize<br />
   
- Testing data <br />
Since, the original dataset does not provide the ground truth label for testing data. <br />
In our experiment, we split the training data into training and validation set, then use the validation data as our testing set. <br />
The splitting proportion is 75:25 for training and validation. <br />

#### Classification Models:
We mainly perform our experiment using two models which are Convolutional Neural Networks (CNN) and Long short-term memory (LSTM).<br />
- Convolutional Neural Networks (CNN) <br />
CNN is a deep learning method which is popular widely used to tackle many complex problems including classification. We utilize CNN model to solve our problem and compare our results received from different settings such as the result without preprocessing application, the result using 14 channels and the result using 32 channels   

- Long short-term memory (LSTM) <br />
LSTM is another high-performanced model in present. While CNN is good at solving many complex problems, LSTM gives an impressive result on time-series data due to its special architecture. We perform the experiments without data-preprocessing, preprocessed data on 11 channels and preprocessed data on 32 channels. For the results in details can be found in the following part.


###  Experiment Settings and Results:
- CNN <br />
![capture_004_14062022_002749](https://user-images.githubusercontent.com/21188544/173400795-b8b4e5e3-4e9e-439b-b13b-d9b66dad840a.jpg)






- LSTM  <br />
![capture_008_14062022_000352](https://user-images.githubusercontent.com/21188544/173396609-ba8d7678-6659-4f34-b0f3-482759bda2ff.jpg)
![capture_001_14062022_002716](https://user-images.githubusercontent.com/21188544/173400849-af9ba0ec-62e2-44ed-bce4-44f34dd9bf54.jpg)
![capture_002_14062022_002731](https://user-images.githubusercontent.com/21188544/173400882-b7505fbc-ce97-4d40-a5fd-78bec393d473.jpg)
![capture_003_14062022_002740](https://user-images.githubusercontent.com/21188544/173400940-f6b047c4-7d7c-4e93-b210-4c5920ee2376.jpg)



### Discussion:

###  Demo:

### Acknowledgements:
- Luciw, M. D., Jarocka, E., & Edin, B. B. (2014). Multi-channel EEG recordings during 3,936 grasp and lift trials with varying weight and friction. Scientific data, 1(1), 1-11. ([PDF](https://www.nature.com/articles/sdata201447))
- Várszegi, K. (2016, October). Comparison of algorithms for detecting hand movement from EEG signals. In 2016 IEEE International Conference on Systems, Man, and Cybernetics (SMC) (pp. 002208-002213). IEEE.([PDF](https://ieeexplore.ieee.org/abstract/document/7844566))
- Li, S., & Feng, H. (2019, July). EEG signal classification method based on feature priority analysis and CNN. In 2019 International Conference on Communications, Information System and Computer Engineering (CISCE) (pp. 403-406). IEEE. ([PDF](https://ieeexplore.ieee.org/abstract/document/8805870))
- Alexandre Barachant, Rafał Cycon. Pushing the limits of BCI accuracy: Winning solution of the Grasp & Lift EEG challenge. 6th International Brain-Computer Interface Meeting, May 2016, Monterey, United States. ⟨hal-01349562⟩ [PDF](https://hal.archives-ouvertes.fr/hal-01349562/)
- Deep Learning for Grasp-and-Lift Movement Forecasting Based on Electroencephalography by Brain-Computer Interface [PDF](https://link.springer.com/chapter/10.1007/978-3-030-80475-6_1)
- Wang, P., Jiang, A., Liu, X., Shang, J., & Zhang, L. (2018). LSTM-based EEG classification in motor imagery tasks. IEEE transactions on neural systems and rehabilitation engineering, 26(11), 2086-2095. ([PDF](https://ieeexplore.ieee.org/abstract/document/8496885))
- 
----------------------------------------------------------------------------
#### Author.
Pattamon Rattanapan  ID 108065436, 林孟萱 ID 110065509, 吳余山 ID 110033408  



