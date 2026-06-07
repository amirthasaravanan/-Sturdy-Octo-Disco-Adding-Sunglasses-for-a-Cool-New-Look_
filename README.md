# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

### Program
```python
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```python
faceImage = cv2.imread("passport size.jpeg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
```python
faceImage.shape
```
```python
#resized_faceImage.shape
faceImage.shape
```
```python
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread("glass.webp", -1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
```python
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(190,50))
print("image Dimension ={}".format(glassPNG.shape))
```
```python
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,2]
```
```python
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
```python
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[225:275, 205:395] = glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
```python
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[225:275, 205:395]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
```python
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[225:275, 205:395]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
```python
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[225:275, 205:395] = glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
### Output

<img width="338" height="435" alt="download" src="https://github.com/user-attachments/assets/e2397917-f5f2-4b49-9612-cfe8ded237d8" />



<img width="561" height="303" alt="download" src="https://github.com/user-attachments/assets/d719507f-548b-4ddc-b883-d921b5c06a87" />




<img width="1209" height="205" alt="download" src="https://github.com/user-attachments/assets/caaa43e1-b6c8-4ee5-a771-38053a2b031f" />





<img width="338" height="418" alt="download" src="https://github.com/user-attachments/assets/89cfbc9a-27b0-4991-9859-7d43deca90be" />




<img width="1597" height="186" alt="download" src="https://github.com/user-attachments/assets/26a9e1f1-b90f-453f-b804-af9d67f0d40a" />



<img width="1606" height="988" alt="download" src="https://github.com/user-attachments/assets/e0f8ee12-a7a6-4895-be96-1931a1b3e90c" />
