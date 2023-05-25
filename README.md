# PPD: Heart Rate Measurement Through Video Analysis 

Heart rate measurement utilizing the green channel of pixels is referred to as photoplethysmography (PPG). PPG is a non-invasive approach that utilizes light to detect variations in blood volume. The green channel is commonly selected due to its ability to effectively capture blood volume changes while minimizing the impact of motion.

The process of heart rate measurement through video analysis using the green channel of pixels consists of the following steps:

### 1. Video acquisition 
For this project, a standard smartphone camera was used to obtain video footage of a person's face standing in front of a white wall. The videos were taken under proper lighting conditions.

### 2. Face detection 
In this application, a Haar cascade classifier was utilized to detect frontal faces in each video frame. The cascade classifier is built upon Haar-like features and the AdaBoost algorithm. This type of classifier is a machine learning-based object detection algorithm. It uses Haar-like features, which are simple rectangular features calculated by comparing pixel intensities in different image regions. These features capture local intensity variations and can be efficiently calculated using integral images. 

OpenCV offers a range of pre-trained Haar cascade classifiers, and in this particular instance, the **'haarcascade_frontalface_default.xml'** was employed. In addition, the **detectMultiScale()** function was used to obtain the coordenates of the rectangles containing the detected fases (ROI). The parameters used in this function were:

**_- image:_** The input frame in grayscale format.

**_- scaleFactor:_**  This parameter was set to 1.6 because a smaller value increased false positives as the algorithm detected smaller faces. 

**_- minNeighbors:_** This parameter was set to 5, indicated the minimum number of neighbors (rectangles) required for a detected region to be considered a face. A higher value resulted in missed faces. 

### 3. Green channel extraction
To extract the green channel of the pixels in the face, the ROI (Region of Interest) of each frame was obtained with the **detect_roi()** function. In order to reduce errors at the beginning of the recording, the first 10 seconds of the video were excluded. After the green channel of the ROI was extracted, the average value of the normalized channel was added to the variable that contains the signal. 

Normalizing the green channel is necessary to ensure that the pixel intensities are within a consistent range, in this case between 0 and 255. This is because different images may have different intensity ranges due to variations in lighting conditions or camera settings. By normalizing the intensities, we can better compare pixel values across different images and ensure that our signal processing techniques are applied consistently. The function **cv2.normalize()** was used to scale the intensity values of the green channel to the desired range. 

The purpose of calculating the average value of the color channel intensities within the selected ROI is to obtain a single scalar value that represents the color information of the frame. By doing this, the code reduces the dimensionality of the color information in the ROI from a 2D array of pixel values to a 1D array of scalar values, which is easier to work with and process. Additionally, by using the mean value instead of individual pixel values, the code is less sensitive to small variations in pixel intensity and noise, which can improve the robustness of the heart rate measurement.

### 4. Signal processing
A bandpass filter was used to remove noise and unwanted frequencies from the green channel signal. The purpose of this process was to isolate the frequency range specifically associated with the heart rate, while simultaneously reducing or attenuating any noise occurring outside that range. Because of this, the chosen cutoff frequencies correspond with the typical resting heart rate of a person (60 t0 100 BPM). 

### 5. Heart rate estimation using Fourier Analysis
Once the green channel signal was preprocessed, the Fast Fourier Transform was applied to the signal. This proccess  decomposes the signal into frequency components, obtaining its frequency spectrum. The frequency spectrum obtained was analyzed to identify the dominant frequency that corresponds to the heart rate. This was done by finding the peak with the highest magnitude in the spectrum using the **find_peaks()** function from the SciPy library. Finally, the frequency was converted into beats per minute (BPM), providing a numerical value representing the estimated heart rate.
