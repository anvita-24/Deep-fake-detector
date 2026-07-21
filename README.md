# DeepFake_Detection
## Table of Contents:
- What is DeepFake?
- Demo of the Project
- Impact of DeepFake Videos
- Project Objectives
- Project Pipeline
  - Pre-processing WorkFlow
  - Prediction WorkFlow
- Models Usage and their Architecture
- Deploy
  - Code Running Commands
- Technologies Used
- Conclusion
- Team


## What is DeepFake?
- DeepFakes are images or videos in which a person's face has been replaced with
someone else's, produced by an AI-driven DeepFake converter — essentially an
advanced form of face swapping.
- Most DeepFakes are created by blending or superimposing existing images onto
source images and videos using Generative Adversarial Networks (GANs), and these
networks keep improving in quality every day.


## Impact of DeepFake Videos
- DeepFakes can be used to spread fake news, produce misleading celebrity or
political content, and enable financial fraud.
- False rumors spread through DeepFake videos can cause public unrest and mental
distress among viewers.
- The film industry, content platforms, and social media companies are actively
working to counter the spread of DeepFake content.
 
 # Project Objectives:
 
Identifying DeepFakes is essential to prevent the misuse of AI technology.
We aim to:
-  Build a model that processes a given video and classifies it as REAL or FAKE.
-  Deploy a feature within social media apps that can detect and warn content
providers attempting to upload DeepFaked images or videos before they go viral.

![image](https://user-images.githubusercontent.com/77656115/206965843-6ac74168-3e31-43d6-9bbf-3e3d25e17522.png)

### Goal:
To create a deep learning model capable of recognizing DeepFake images through
thorough analysis of video frames, identifying subtle imperfections in the face and
head so the model learns what distinguishes a real image from a DeepFake.

![image](https://user-images.githubusercontent.com/77656115/206965890-a1c345cf-8ae9-49f7-b498-ae4c7168666a.png)

### Project Pipeline

| Steps | Description |
| --- | --- |
| Step1 | Loading the datasets |
| Step2 | Extracting videos from the dataset |
| Step3 | Extracting all frames from the video for both real and fake samples |
| Step4 | Recognizing the face sub-frame |
| Step5 | Locating the facial landmarks |
| Step6 | Frame-by-frame analysis to detect changes in facial landmarks |
| Step7 | Classifying the video as REAL or FAKE |


## General WorkFlow:
### Pre-processing:
![image](https://user-images.githubusercontent.com/77656115/206968030-1e9729e7-8d34-4295-a110-d05ad0ade7bb.png)

### Prediction WorkFlow:
![image](https://user-images.githubusercontent.com/77656115/206968272-73db6238-79a0-46a1-ad5b-e651ad002322.png)

# Models Usage: 
### Models with CNN Architecture

The following models with CNN architecture were implemented:

**MesoNet**
- Pre-trained to detect DeepFake images, but performs poorly when detecting fake
video frames.

**ResNet50**
- Trained on DeepFake images cropped from videos, initialized with pre-trained
ImageNet weights.

**EfficientNetB0**
- Also trained on DeepFake images cropped from videos, initialized with pre-trained
ImageNet weights.

### Models with CNN + Sequential Architecture
**InceptionV3 (CNN Model) + GRU (Sequential)**

-  Performs well due to the combination of CNN and sequential architecture.
- Test accuracy is approximately 82%.
- Generates a feature vector for each frame in the video.
- Hyperparameters used:
  - Optimizer: Adam (adapts the learning rate over time, which works well here)
  - Metric: Accuracy
  - Loss: sparse_categorical_crossentropy (suited for two or more label classes)
- Adam performed better than the other optimizers tested.
- Accuracy improves as the number of training epochs increases.

**Limitations**
This model doesn't perform well when multiple faces appear in the video, since it
needs to detect and track multiple faces within each frame.

**EfficientNetB2 (CNN Model) + GRU (Sequential)**

- Performs well due to the combination of CNN and sequential architecture.
- Test accuracy is approximately 85%.
- Generates a feature vector for each frame in the video.
- Hyperparameters used:
  - Optimizer: Adam (adapts the learning rate over time, which works well here)
  - Metric: Accuracy
  - Loss: sparse_categorical_crossentropy (suited for two or more label classes)
- Adam performed reliably well across training.
- Accuracy improves as the number of training epochs increases.

**Limitations**
- This model doesn't perform well with dark or poorly lit video backgrounds, as face
detection becomes difficult under low-light conditions.

## Running Code
- A combination of CNN and RNN models is used to detect fake videos. We achieved
a test accuracy of ~85% on a sample DFDC dataset.
- To run this code, first install the dependencies:
```bash
  pip install -r requirements.txt
```

**Run the main.py file in the deploy folder**
```bash
  python main.py
```
*Make sure all required packages are installed, and running on a GPU is recommended. Results are typically returned within about a minute for a 10-second, 30fps video.*

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.w3schools.com/css/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="40" height="40"/> </a> <a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/> </a> <a href="https://opencv.org/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/opencv/opencv-icon.svg" alt="opencv" width="40" height="40"/> </a> <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://scikit-learn.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="scikit_learn" width="40" height="40"/> </a> <a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://seaborn.pydata.org/_images/logo-mark-lightbg.svg" alt="seaborn" width="40" height="40"/> </a> <a href="https://www.tensorflow.org" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/tensorflow/tensorflow-icon.svg" alt="tensorflow" width="40" height="40"/> </a> </p>

## Conclusion:

- In this project, we implemented a method for detecting DeepFake videos using a
combination of CNN and RNN architectures, with a focus on face-swapped DeepFake
videos.

- We initially experimented with pre-trained CNN models such as EfficientNet and
ResNet, computing the probability of each video frame being fake and predicting the
final output based on an aggregate of these probabilities. However, the results were
not satisfactory, which led us to combine CNN and RNN models instead.

- In the CNN + RNN approach, features from face-cropped video frames are extracted
using pre-trained CNN models and passed to an RNN model that classifies the video
as REAL or FAKE. We experimented with EfficientNet and InceptionV3 for feature
extraction, with GRU used for the final classification. This approach achieved a
maximum test accuracy of ~85%, with notably high precision on FAKE videos —
achieved by including a higher proportion of FAKE videos during training.
