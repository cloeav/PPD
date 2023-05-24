# PPD: Heart Rate Measurement Through Video Analysis 

Heart rate measurement utilizing the green channel of pixels is referred to as photoplethysmography (PPG). PPG is a non-invasive approach that utilizes light to detect variations in blood volume. The green channel is commonly selected due to its ability to effectively capture blood volume changes while minimizing the impact of motion artifacts.

The process of heart rate measurement through video analysis using the green channel of pixels consists of the following steps:

### 1. Video acquisition 
For this project, a standard smartphone camera was used to obtain video footage of a person's face standing in front of a white wall. The videos were taken under proper lighting conditions.

### 2. Face detection 





The purpose of calculating the average value of the color channel intensities within the selected ROI is to obtain a single scalar value that represents the color information in the region of interest. This is done by taking the mean value of the intensities across all the pixels in the ROI.

By doing this, the code reduces the dimensionality of the color information in the ROI from a 2D array of pixel values to a 1D array of scalar values, which is easier to work with and process. Additionally, by using the mean value instead of individual pixel values, the code is less sensitive to small variations in pixel intensity and noise, which can improve the robustness of the heart rate measurement.


Normalizing the green channel is necessary to ensure that the pixel intensities are within a consistent range, typically between 0 and 255. This is because different images may have different intensity ranges due to variations in lighting conditions or camera settings. By normalizing the intensities, we can better compare pixel values across different images and ensure that our signal processing techniques are applied consistently.

In the code provided, cv2.normalize is used to scale the intensity values of the green channel to the range of 0-255.
