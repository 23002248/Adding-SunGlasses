# Adding-SunGlasses
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


# Import libraries
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
# Load the Face Image
```
faceImage = cv2.imread(r"C:\Users\admin\OneDrive\Pictures\photo 1.jpg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="507" height="577" alt="image" src="https://github.com/user-attachments/assets/9f1ffc76-cedb-423f-9b06-11f607a4a150" />

```
faceImage.shape
(886, 689, 3)
```

# resized_faceImage.shape
```
faceImage.shape
(886, 689, 3)
```
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread(r"C:\Users\admin\Downloads\sunglass-png-aviator-sunglass-png-pic-627.png",-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="747" height="387" alt="image" src="https://github.com/user-attachments/assets/75738788-87a3-4274-9768-4444b560c9d0" />

```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(250,100))
print("image Dimension ={}".format(glassPNG.shape))
image Dimension =(100, 250, 4)
```
```
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1359" height="325" alt="image" src="https://github.com/user-attachments/assets/d64a7cfa-bfcc-4f31-bf37-338f48fd5216" />

```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()
```
```
# Replace the eye region with the sunglass image
faceWithGlassesNaive[230:330,220:470]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="473" height="549" alt="image" src="https://github.com/user-attachments/assets/f9fedb65-673c-4943-9250-53c56267ab26" />

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[230:330,220:470]

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
<img width="1380" height="243" alt="image" src="https://github.com/user-attachments/assets/73bcb1b3-b0f7-48f9-9104-ef43e5dc86ce" />

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[230:330,220:470]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="1109" height="674" alt="image" src="https://github.com/user-attachments/assets/ee2dcf96-b3fe-442e-810b-dc5827473b0b" />


# Result:
Thus Adding Sunglasses to Your Passport Photo Using OpenCV is executed successfully


