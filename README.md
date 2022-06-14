![capture_001_02062022_01551122](https://user-images.githubusercontent.com/21188544/171472880-b9909c94-5293-477d-9443-7f5620cfcaa2.jpg)

# Final Project
## Grasp-and-Lift-Detection-on-EEG
This is project for fulfilment of the course Brain Computer Interfaces and Application. <br />
National Tsing Hua University, Taiwan, R.O.C, Spring Semester 2021. <br /> <br />

### Materials
Project proposal: [Here](https://docs.google.com/presentation/d/17Lb9k7V1zG_rWtpeJskX08m1WGs6smFaxS5O0AqAxZ8/edit?usp=sharing)<br />
Project demo slide: [Here](https://docs.google.com/presentation/d/1fxHWNvNH8yGjF1S2BwcqpV5jJlt2WBBM5NpfJ-hYSlU/edit?usp=sharing)

----------------------------------------------------------------------------
### 1. Introduction
![capture_001_02062022_030150](https://user-images.githubusercontent.com/21188544/171482094-eae8c6ea-ebeb-4df1-8442-c8b805d3283a.jpg)
After the first EEG data was record in 1924 by Hans Berger, a German psychiatrist. There are many researches developed based on EEG data, since EEG data is rich in infortaion and containing all body activities in term of signal. BCI is also one popular research domain that mainly developed based on EEG data with an intention to help people to be able to directly control the computer from the brain. Especially, for people with disabilities, BCI helps to enhance their life quality to live more independently and more convenient.<br />

In this project, we implement and develop the machine learning approach to classify the different hand movements using EEG data.This challenge was a research prediction competition on Kaggle in 2015, which the competition result can be found [here ](https://hal.archives-ouvertes.fr/hal-01349562/)<br />
For more information about the competition, [Pleas click here ](https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data)

----------------------------------------------------------------------------

### 2. Project objective:
1. To find the significant features that can improve the model performance.
2. To implement the classification model to accurately classify the different hand movements by using EEG signals.
3. To find the high heavyweight channels, cancel other channels to increase the efficiency of the model.<br />
 
----------------------------------------------------------------------------

### 3. Dataset:
We use 'Grasp-and-Lift EEG Detection (GAL) dataset' (Luciw, Jarocka & Edin, 2014) as our dataset. <br />
The paper was published in 2014 and the dataset was used for a prediction competition on Kaggle in 2015. <br />

Apart from the competition, this data is also used for many studies for example to compare the performance of algorithm  
to detect hand movement from EEG data (Várszegi, K., 2016), to improve the classification method on EEG data using 
feature priority based analysis and CNN in 2019 (Li et al., 2019),and to forecast Grasp-and-Lift Movement (Gordienko et al., 2021), 

This dataset not contains only EEG data but also includes EMG data and 3D of both hand and object position.  <br />
However, in this study, we will focus on EEG data only. The brief information of the dataset is shown below; <br />
  - 12 participants, 10 series of trial subjects and ~ 30 trials on each series, 3,960 trials in total.<br />
  - 6 labels: Hand Start, First Digit Touch, Both Start Load Phase, Lift Off, Replace, Both Released.
  - Object used and action:
    -  different weight (165, 330, 660 g).
    -  different surface (sandpaper, suede, silk surface).
    -  different action e.g. enforcing change in fingertip, grasp with thumb and index finger and  lift and hold.
For data collection, this dataset is recorded using EEG sensor ActiCap 32 channals in conjunction with BrainAmp EEG signal amplifier. After preprocessing, the ready to use data sample rate is 500 Hz.
        
![capture_001_13062022_014953](https://user-images.githubusercontent.com/21188544/173246397-fa775461-8c87-4b51-9361-91c28a9a5603.jpg)
Figure1 displays the EEG map of ActiCap and the location of each channel. For our task, we are going to classify the different hand movement which is controlled by primory motor cortex and primary sensory cortex, figure 2. So, we will focus on using the data which location is on these part of the brain which are in highlight area.

To download the file, please visit [folder data](https://github.com/rickylk/LSTM-based-method-for-grasp-and-lift-detection-on-EEG/tree/main/data) or [click]( https://www.kaggle.com/competitions/grasp-and-lift-eeg-detection/data) <br />
For more information about the dataset collection methodology, please refer to [click](https://www.nature.com/articles/sdata201447) <br />

----------------------------------------------------------------------------
### 4. Methodology: 

#### 4.1 Data Preprocessing:
![capture_006_13062022_223220](https://user-images.githubusercontent.com/21188544/173377539-f0caa1d4-efcb-4f1e-a294-2d9b736a7fb4.jpg)
From figure 3, we visualize the raw data using EEGlab. We can see that the raw data contains a lot of artifacts for example the eye blinking that clearly display in channel 1,2,3 and 4. To remove these artifacts will help to improve the quality of our data before feeding them to the next process of feature extraction and classification. We apply multiple method of preprocessing as following;
- Preprocessing<br />
   -  Lowpass filter <br />
      -  The lowpass filter can allow the EEG signals with frequency lower than the cut-off frequency to pass through it. It is a good method to remove noise from the data. The cut-off frequency in the experiment of LSTM part is 35 Hz.
   -  Bandpass filter <br />    
      - The bandpass filter allows the selected range of frequencies to pass the filter and remove the unwanted frequencies of signal. Bandpass filter also helps to optimize the signal-to-noise ratio, or in other words improve the quality of the signal. In the experiment, bandpass filter range is 1-50 Hz. 
   -  Beta filter   <br />  
      - Similar to bandpass filter, using the filter of Beta frequency range, 12-30 Hz.   
   -  Fast Fourier transform (FFT)<br />
      - FFT is the algorithm that calculate the discrete fourier transform of a sequence. FFT converts the digital signal data from time domain to frequency domain 
   -  Standardize<br />
      - Standardization can make features become standard normally distributed data and help model converge quickly and improve the accuracy of model.
   -  Linear regression<br />
      - From the method of Wang (Wang et al., 2018), they use 1d-AX to preprocess data and then use LSTM to predict the result. When calculating the features using 1d-AX, they always divide the signal into segments of equal length, apply linear regression on every segment and get the slope and mean. In the experiment of LSTM part, we use the first two steps to preprocess the EEG data. By this way, the signal becomes smoother and some noise can also be removed. <br /> 
      - To find the best length for each segments, we try different lengths (100/50/25) and compare the results.
   -  Polynomial regression<br />
      - Polynomial regression is similar with linear regression, but the degree of linear regression is 1 and polynomial regression is more than 1. In the experiment of LSTM part, we try different degree. When the training data with 32 channels, the degree of polynomial regression is 4. When the training data with 11 channels, the degree of polynomial regression is 2. <br />
      - In addition, we also try different lengths of segments (100/50/25) and compare the results.<br />
      - The following figure shows how the changes after the application of linear regression and polynomial regression
![capture_008_14062022_000352](https://user-images.githubusercontent.com/21188544/173396609-ba8d7678-6659-4f34-b0f3-482759bda2ff.jpg)

   
- Testing data <br />
Since, the original dataset does not provide the ground truth label for testing data. <br />
In our experiment, we split the training data into training and validation set, then use the validation data as our testing set. <br />
The splitting proportion is 75:25 for training and validation. <br />

#### 4.2 Classification Models:
We mainly perform our experiment using two models which are Long short-term memory (LSTM) and Convolutional Neural Networks (CNN).<br />
- Long short-term memory (LSTM) <br />
LSTM is another high-performanced model in present. While CNN is good at solving many complex problems, LSTM gives an impressive result on time-series data due to its special architecture. We perform the experiments without data-preprocessing, preprocessed data on 11 channels and preprocessed data on 32 channels. For the results in details can be found in the following part.

- Convolutional Neural Networks (CNN) <br />
CNN is a deep learning method which is popular widely used to tackle many complex problems including classification. We utilize CNN model to solve our problem and compare our results received from different settings such as the result without preprocessing application, the result using 14 channels and the result using 32 channels   


----------------------------------------------------------------------------
###  5. Experiment Settings and Results:
We used 3 preprocessing methods and 3 set of different numbers of channels for the experiments.We utilize  FFT, Beta and Bandpass filter for [1:50] to preprocess the data for CNN model.  By applying FFT, it will convert the data and we can visualize it to see in term of frequency distribution. Second, beta wave is also a part of FFT, which frequency is between [12:30], beta wave is useful for motion classification. Last, Bandpass filter, the filter helps to eliminate noise in the data.<br /> 

GAL dataset contains 32 channels in total. However, our task is focusing on hand motion classification, which is mainly controlled by the primary motor cortex and primary sensory cortex. Therefore, we perform the experiments using 3 settings:

1. 11 channels, which are C3, C4, Cz,T7, T8, TP9, TP10, CP1, CP2, CP5, CP6.
2. 14 channels, which are FC1, FC2, FC5, FC6, C3, C4, T7, T8, TP9, TP10, CP1, CP2, CP5, CP6.
3. All 32 channels. 

#### 5.1 LSTM  <br />
   -  Because LSTM is good at processing time-series data, we use the previous two seconds of data to predict the next point’s event. The sample rate of our dataset is 500 Hz, so there are totally 1000 points as the input to the LSTM. To reduce the input data, we subsample the input data and the subsample rate is 1/50 points. Therefore, the input data can be reduced to only 20 points. <br />
   -  In our dataset, most labels are [0 0 0 0 0 0]. This means that most of the time nothing happens. To focus on event prediction, we remove the labels of [0 0 0 0 0 0] and compare the accuracy when model predict the events. <br />
   -  The below tables show the result of LTSM model. We compare the effect of different channels and preprocessing methods on the results. <br />
   -  From the results of 32 channels, it can be found that when the data preprocessed with lowpass filter and standardization, the accuracy is not improved but decreased. However, lowpass filter and standardization significantly improve the accuracy of 11 channels. In addition, we also use PCA to reduce the dimension of 32 channels to 11 channels. From the result, the accuracy of 11 channels is better than 32 channels with PCA. We think it is because PCA may distort original data and decrease the accuracy. <br />
![capture_004_14062022_130105](https://user-images.githubusercontent.com/21188544/173497282-ebb32a60-419b-4a5b-a1c8-7dc75651df52.jpg)
   -  In the method of Wang (Wang et al., 2018), they use 1d-AX to replace bandpass filter when preprocessing signal. Therefore, we compare the accuracy with and without lowpass filter when applying linear regression on the data. <br />
   -  From the below results, when we use the data with 32 channels, the accuracy with lowpass filter is better. However, the results are reversed under 11 channels. We think this means that when more channels we use, linear regression can’t completely replace the lowpass filter. About the result of segments with different length, we found the overall best accuracy is using segments with 50 points. We think this result is closely related with the subsample rate which is 1/50 points. It may have different result when using different subsample rate. <br />
![capture_002_14062022_002731](https://user-images.githubusercontent.com/21188544/173400882-b7505fbc-ce97-4d40-a5fd-78bec393d473.jpg)
   -  The overall results of using polynomial regression is worse than linear regression, especially using the data with 32 channels. We think this is related to the degree of polynomial regression. In the experiment, the degree of 32 channels is 4 and the degree of 11 channels is 2. This result shows when using regression with higher degree, the less noise will be removed. <br />
![capture_003_14062022_002740](https://user-images.githubusercontent.com/21188544/173400940-f6b047c4-7d7c-4e93-b210-4c5920ee2376.jpg)
   -  In conclusion, from the results, when using data with 32 channels, the best accuracy is 0.6956. The preprocessing methods are lowpass filter, linear regression and standardization. The length of segments for linear regression is 50 points. When using data with 11 channels, the best accuracy is 0.5181. The preprocessing methods are linear regression and standardization. The length of segments for linear regression is also 50 points. <br />

#### 5.2 CNN <br />

From the result below, we can see that beta preprocessing results in the highest score in Train_acc, Test_acc and Test1_acc with the accuracy of 0.865, 0.937 and 0.449 respectively, while the highest score among all is obtained by Train_acc with beta preprocessing on 32 channels.  <br />

With Bandpass filter preprocessing, the highest score of 0.845 is achieved by Train_acc on 14 channels and with FFT preprocessing, the highest score with accuracy of 0.856 is from Train_acc on 14 channels. <br />
![capture_005_14062022_143306](https://user-images.githubusercontent.com/21188544/173509028-931ddc4d-4f47-4f3d-813f-cc4e40d3eb1c.jpg)

----------------------------------------------------------------------------

### 6. Discussion:
In the experiment of LSTM, when training the model, the training accuracy and validation accuracy are almost above 85% under 11 channels and 32 channels. However, the testing accuracies drop significantly. The best testing accuracy of 11 channels is only 51%, and the best testing accuracy of 32 channels is only 69%. About this problem, we think it is because the model has already overfit. To solve this problem, there are some common methods, such as simplifying the model and early stop. We will try these methods in the future to improve the current results. <br />

From the results of different channels, it is obvious that using data with 32 channels is better than 11 channels. We think this is quite reasonable because data with 32 channels contain more features. Though the result of 11 channels is not good enough, it shows these 11 channels is important for classifying hand movements. <br />

With LSTM model, we can see that with 11 channels, the accuracy is not as high as others, indicating that the data from 11 channels is not efficient enough to perform a good classification on 6 different hand movements. Therefore, we adjust the number of channels to 14 and perform our experiments again on CNN model. <br />

For CNN model, from the result shown in table above, with FFT application, the training accuracy is highest among other accuracy on both 14 channels and 32 channels. While the validation accuracy is high, the testing accuracy and testing1 accuracy are comparatively lower. These scores indicate that the training data is easier to classify than the validation and testing data.The validation accuracy of FFT application is also the highest among other preprocessing method on both 14 channel and 32 channels. <br />

For Beta preprocessing of 32 channels, the testing accuracy is very high at the score of 0.834 and dropping to 0.379 on testing1 accuracy. This is because the testing accuracy uses the six-digit label [0 0 0 1 0 0] which is very large compared to using the label as 1 digit, for example, label 1,2,3,4,5 or 6. For binary classification, when the label contains 6 digits, with the ratio of 1 and 0 is 1:5. The model is more likely to fit the number 0 than 1. Therefore, the result of the model performs better on testing accuracy than testing1 accuracy, that converts the label from 6 digits to 1 digit. The concept of beta filter is also a part of FFT,, to implement beta filter also gives similar result compared to FFT application.   <br />


In summary, the experiment with LSTM model using multiple preprocessing methods give normal performance on 6 different hand movements using 32 channels while the score archieved by using 11 channels is significantly lower than using 32 channels. We can assume that the data of 11 channels does not contain enough information to train the model and predict the label efficiently. With CNN model, the best performance is obtained from bandpass filter preprocessing in training accuracy, testing accuracy and testing1 accuracy on both 14 and 32 channels. By comparing the result of FFT and beta preprocessing, both two preprocessing method provide similar result due to the similarity in concept as beta is a part of FFT. However, in some settings, the are a large gap between the training and testing accuracy, this also indicating that the model may become overfitting since the model perform a lot better on the data it uses to train and make more error on the data the model never see them before. It also assume that the data used to evaluate the training accuracy and testing accuracy is not highl in its similarity.  

----------------------------------------------------------------------------
### 7. Demo:

https://user-images.githubusercontent.com/21188544/173550625-761b8887-fbb9-4b8d-ad2f-455313958f2f.mp4

----------------------------------------------------------------------------
### 8. Acknowledgements:
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



