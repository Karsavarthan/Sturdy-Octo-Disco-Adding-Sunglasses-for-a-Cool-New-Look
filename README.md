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

## PROGRAM & OUTPUT:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

```
faceImage = cv2.imread('Karsa.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![Screenshot 2025-03-14 110250 1](https://github.com/user-attachments/assets/552630be-16a0-4683-adf1-d5ff4bcd994c)

```
faceImage.shape
```
![! Screenshot 2025-03-14 110300 1](https://github.com/user-attachments/assets/e4a49912-8a82-4bc2-ac14-6f425f8b7c52)


```
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

![! Screenshot 2025-03-14 110260 1](https://github.com/user-attachments/assets/988ee5fa-b61d-4df5-86bd-54807a555247)


```
glassPNG = cv2.resize(glassPNG,(590,250))
print("image Dimension ={}".format(glassPNG.shape))
```

![! Screenshot 2025-03-14 115060 1](https://github.com/user-attachments/assets/cb92dfba-d056-4a07-98f9-ce48d5418168)


```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

```
plt.figure(figsize=[35,35])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![! Screenshot 2025-03-14 120360 1](https://github.com/user-attachments/assets/39e16c2d-0794-4704-bb15-6b19db95b47d)

```
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[750:1000, 710:1300]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

```
![! Screenshot 2025-03-14 195260 1](https://github.com/user-attachments/assets/f3a91a2e-3041-4021-ad08-211f5458d9fb)


```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[750:1000, 710:1300]

maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
![! Screenshot 2025-03-14 1195624 1](https://github.com/user-attachments/assets/9db9a9f8-dcf9-47d0-abe5-809d47a7ec47)

```
faceWithGlassesArithmetic[750:1000, 710:1300]=eyeRoiFinal

plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

![! Screenshot 2025-03-14 195612 1](https://github.com/user-attachments/assets/195d9763-a5be-4b45-b22b-7a14c1dc6d49)


