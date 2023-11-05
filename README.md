# face-mask-detector

This project was undertaken by Jathin Pranav Singaraju and Lavik Jain during the UT Dallas Advanced AI Workshop. The results have been cited globally in the [*Journal of King Saud University*](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8786444/).


## Purpose and Goal

The novel Coronavirus has devastated the world in the past couple of months. The pandemic has caused major destruction to the business, travel, and technology industries and has taken the lives of many people. Its imprint will forever be engraved in our history due to its worldwide impact. In order to mitigate these impacts, safety precautions must be followed and one of the major ones is wearing a mask. Therefore, the widespread use of masks will reduce the number of cases and deaths around the world. So, we came up with a way to solve this— a face mask detector. This system can be used in offices, schools, and stores where masks are mandatory. The machine, built from a CNN model, can differentiate between people not wearing and wearing a mask.

## Description
This project is built from a MobileNetV2 framework. It utilizes a dataset with 20,000 images to train and test itself. It only requires 3 epochs to train and reaches maximum accuracies of about 99.9% during the training. The explanation of the process and code will be outlined below:

## Project

### Step 1
#### Obtaining and Converting the Dataset:
The first step is to obtain a dataset. We retrieved it from *Prasoon Kottarathil's "Face Mask Lite Dataset"* that can be found [here](https://www.kaggle.com/prasoonkottarathil/face-mask-lite-dataset/). This dataset has 1024 x 1024 RGB images; however, the size and color of these images greatly impacted the preprocessing and storage of the image pixel arrays. Therefore, we converted the images ourselves into 224 x 224 grayscale. This would also allow the images to be easily fed into the MobileNetV2 model. Since we have already provided you with the modified dataset, you can visit this link [here](https://www.kaggle.com/luka77/facemask-detection-dataset-20000-images/) or [here](https://www.kaggle.com/pranavsingaraju/facemask-detection-dataset-20000-images/) and download the modified dataset that we have made. Both links lead to the exact same dataset.

We ran this conversion by creating the convert_images.py file. If you want to use *Prasoon's* dataset please use convert_images.py to convert the images and then proceed. Please follow along with the comments in the code, to guide you. You do not need to run convert_images.py if you use either of the two kaggle links (224 x 224 grayscale images dataset) provided above. This conversion step is for people who want to use *Prasoon's* dataset and run it from the beginning.

<p align="center">
  <img src="https://docs.google.com/drawings/d/e/2PACX-1vS53Lc61_LGZeOPqavdQvjss4vHrN9Gf6bfe79hP_gE548xhIZgTwr2n0Da46yVhKxwpLJOniUQ_boG/pub?w=762&h=649">
 </p>
 
### Step 2
#### Load the Images and Pre-Process:
This is the next step after you have received and unzipped the datasets from the kaggle link. At this point, you should have two directories for the 224 x 224 images (one for mask and one for no mask). Follow along with the comments in process_data.py in order to understand the process. It describes the code step-by-step, making it easy to understand. This file basically pre-processes the images and puts them into arrays to be used later when training the model. We made our own progress bar to show the progress of importing the images. The file, progress_bar.py, has the code to the progress bar and is also completely commented to explain the steps.

### Step 3
#### Train the Model:
After preprocessing the data, saving the pixel values into arrays, and storing labels, we can begin to make the model. Once again, the code uses a MobileNetV2 architecture, which is meant to have good accuracy rates. It combines a base model with layers that you can choose to use in order to make the model optimized. The testing and training split also occurs here, as we are doing an 80/20 (training/testing) split. We experimented with the learning rate, epochs, and batch size in order to best fit our data. This does take some time, please be patient. Additionally, the model uses data augmentation to improve the model accuracy, because it trains the model against a couple of random images, in order to ensure that it can detect images in random cases. The explanation for the whole model can be seen in the comments of main_model.py. Lastly, the model stores the accuracy, loss, and some more data for the best epoch and saves that model into your current working directory. We have already made the model and trained it, so need to be done on your behalf. However, if you do want to retrain the model with our data, or even your data, check the split ratio and experiment with the model params. All the code is explained very clearly in main_model.py so it should be easy to get the significance of each line. You don't have to run main_model.py if you want to just test it with your own images. All you have to do if you want to test is to run video_testing.py. The architecture of our model is below:

<p align="center">
  <img src="https://docs.google.com/drawings/d/e/2PACX-1vRHXy676k_VvCpqb0PR7O0BW9mslYivTk5TeRd2uqOU_WJrXfYGdu3uLSdokpqLv1Cb9qqoXB1DKQiT/pub?w=800&h=715">
 </p>

### Step 4
#### Testing the Model:
This is the only step that you need to perform on your behalf if you want to run the code and see it working real-time. All the correct packages need to be imported. This testing phase uses cv2 video stream to recognize each frame in the image and classify all the people with and without masks. This program constructs blobs of each frame and passes it through a pre-trained face recognition model with weights (both files can be found in face-detection-models) in order to find all the faces in a frame. It then finds the ROIs (region of interests) and draws bounding boxes on them for aesthetics. The ROIs will be the part we are interested in, so that we can classify mask or no mask. Also, it shows the color and label on top of the box, along with a probability of the model confidence. After testing different face recognition methods, we noticed that Haar cascading was found to be inaccurate and not reliable because it wouldn't find the ROIs most of the faces with masks. Face detection using the caffe model is super precise and notices the faces almost every single test run. So if you are looking for an accurate face mask predictor, please feel free to try it yourself and share the project. Once again, for a complete understanding of each line in the code, please view video_testing.py. Hope you got it to work and understand everything! Good luck experimenting!

### Extra
#### Notes:
<ul>
<li><p>When you decide to fork this repo and work on it, please cite this github repo link and either of our dataset links for credibility and copyright purposes. Before using our dataset, please read over the license link below.</p></li>
<li><p>Please read the comments in the code in order to completely get an understanding of what this model does and its purpose. The comments are very detailed and should explain what each line's significance and purpose are.</p></li>
<li><p>Please feel free to fork this repo and share it! Thank You!</p></li>
</ul>

#### Special Thanks To:
<ul>
<li><p><i>Dr. Jey Veerasamy</i>, Director, Center for Computer Science Education & Outreach at UT Dallas</p></li>
<li><p><i>Dr. Anurag Nagar</i>, Assistant Professor at UT Dallas</p></li>
<li><p><i>Ashutosh Senapati</i>, MSCS at UT Dallas</p></li>
<li><p><i>Omeed Ashtiani</i>, PhD student in Computer Science at UT Dallas</p></li>
</ul>
<ul>  
<li><p><i>Adrian Rosebrock</i> from <i>PyImageSearch</i></p></li>
<li><p><i>Prasoon Kottarathil</i> for his original dataset</p></li>
</ul>

#### Project Links:
<ul>
<li><p>This GitHub Link: https://github.com/lavikj/Face-Mask-Detection</p></li>
<li><p>Lavik Jain Kaggle Link: https://www.kaggle.com/luka77/facemask-detection-dataset-20000-images</p></li>
<li><p>Pranav Singaraju Kaggle Link: https://www.kaggle.com/pranavsingaraju/facemask-detection-dataset-20000-images</p></li>
<li><p>Prasoon Kottarathil Kaggle Link: https://www.kaggle.com/prasoonkottarathil/face-mask-lite-dataset</p></li>
<li><p>Adrian Rosebrock PyImageSearch Link: https://www.pyimagesearch.com/2020/05/04/covid-19-face-mask-detector-with-opencv-keras-tensorflow-and-deep-learning</p></li>
<li><p>Dataset License Link (CC BY-SA 4.0): https://creativecommons.org/licenses/by-sa/4.0</p></li>
</ul>

## Demo
Below is our linked video and presentation:

Presentation link is [here](https://docs.google.com/presentation/d/1g_97E7p7wfVq2Mczl9HXV0UFrqwkSsLMKyvj1OaXrs0/edit?usp=sharing). </br>
Below is the youtube video for our system, if that does not work, please click [here](https://youtu.be/raveTUuTft0).

[![Face Mask Detection System](https://img.youtube.com/vi/RcaZgubCRrE/0.jpg)](https://youtu.be/raveTUuTft0)
