# EXP.NO-1:Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:

Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  

2) Adjust the brightness of an image.  

3) Modify the image contrast.  

4) Generate a third image using bitwise operations.

## Software Required:

- Anaconda - Python 3.7
- 
- Jupyter Notebook (for interactive development and execution)

## Algorithm:

### Step 1:

Load an image from your local directory and display it.

### Step 2:

Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:

Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:

Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:

Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:

- **Name:** Piritharaman R
- **Register Number:** 212223230148

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

```
bgr_img = cv2.imread('Eagle_in_Flight.jpg')
```

#### 2. Print the image width, height & Channel.
```
bgr_img.shape
```
```

bgr_img.size
```

#### 3. Display the image using matplotlib imshow().
```
plt.imshow(bgr_img,cmap="gray")
plt.title('BGR Image')
plt.axis('on')
plt.show()

```
```
rgb_color_img = cv2.cvtColor(bgr_img, cv2.COLOR_BGR2RGB)
```
```
plt.imshow(rgb_color_img)
plt.title('Color Image')
plt.axis('on')
plt.show()
```
```
plt.imshow(bgr_img[:,:,::-1])
plt.title('Color Image { swapping}')
plt.axis('off')
plt.show()
```


#### 4. Save the image as a PNG file using OpenCV imwrite().
```
cv2.imwrite('output_image.jpg', rgb_color_img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```
jpg_img = cv2.imread('output_image.jpg')

saved_color_img = cv2.cvtColor(jpg_img, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```
saved_color_img.shape
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```

cropped_img = saved_color_img[50:425,200:550]

```
```
plt.imshow(cropped_img[:,:,::-1])
plt.title('Cropped image')
plt.axis('off')
plt.show()
```
```
cropped_img.shape
```

#### 8. Resize the image up by a factor of 2x.
```
resized_img = cv2.resize(cropped_img, None, fx=50, fy=50, interpolation=cv2.INTER_LINEAR)
```
```
resized_img.shape
```

#### 9. Flip the cropped/resized image horizontally.
```
flipped_img = cv2.flip(cropped_img, 1)
```
```
plt.imshow(flipped_img[:,:,::-1])
plt.title('Flipped Image')
plt.axis('off')
plt.show()
```
```
img_eagle_flipped_horz = cv2.flip(cropped_img, 1)
```
```
plt.figure(figsize = [18, 5])
plt.subplot(141); plt.imshow(img_eagle_flipped_horz[:, :, ::-1])
plt.title('Horizontal Flip')
```


#### 10. Read in the image ('Apollo-11-launch.jpg').
```
apollo_img=cv2.imread('Apollo-11-launch.jpg')
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
font_scale=2
color=(255,255,255)
thickness=2
cv2.putText(apollo_img,text,(30,50),font_face,font_scale,color,thickness,cv2.LINE_AA)
rgb_image=cv2.cvtColor(apollo_img,cv2.COLOR_BGR2RGB)
plt.imshow(rgb_image)
plt.axis('off')
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```
x1,y1=400,70
x2,y2=800,600
```

#### 13. Display the final annotated image.
```
rect_color=(255,0,255)
thickness=3
im=cv2.rectangle(apollo_img,(x1,y1),(x2,y2),rect_color,thickness)
img_rgb = cv2.cvtColor(im, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(12,6))
plt.imshow(img_rgb)
plt.axis("off")
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```
boy_img=cv2.imread('boy.jpg')

```

#### 15. Adjust the brightness of the image.
```
bright_image=cv2.convertScaleAbs(boy_img,alpha=1,beta=50) # increase brightness
dark_image=cv2.convertScaleAbs(boy_img,alpha=1,beta=-50) # decrease brightness
plt.figure(figsize=(12,6))
```

#### 16. Create brighter and darker images.
```
value=50
matrix=np.ones(boy_img.shape,dtype="uint8")*value
img_brighter = cv2.add(boy_img, matrix)
img_darker = cv2.subtract(boy_img, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```
# Original Image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(boy_img,cv2.COLOR_BGR2RGB))
plt.title('Original image')
plt.axis('off')
plt.show()
```
```
# Original Image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(boy_img,cv2.COLOR_BGR2RGB))
plt.title('Original image')
plt.axis('off')
plt.show()
```
```
# Brighter image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(img_brighter,cv2.COLOR_BGR2RGB))
plt.title('Brighter image')
plt.axis('off')
plt.show()
```
```
# Darker Image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(img_darker,cv2.COLOR_BGR2RGB))
plt.title('Darker image')
plt.axis('off')
plt.show()
```


#### 18. Modify the image contrast.
```
matrix1 = np.ones(boy_img.shape,dtype="float32")*1.1
matrix2 = np.ones(boy_img.shape,dtype="float32")*1.2
img_higher1 = (boy_img*matrix1).astype(np.uint8)
img_higher2 = (boy_img*matrix2).astype(np.uint8)

```


#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(boy_img,cv2.COLOR_BGR2RGB))
plt.title('Original image')
plt.axis('off')
plt.show()

```
```
# Display the contrast image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(img_higher1,cv2.COLOR_BGR2RGB))
plt.title('Contrast image')
plt.axis('off')
plt.show()
```
```
# Display the Darker image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(img_higher2,cv2.COLOR_BGR2RGB))
plt.title('Darker image')
plt.axis('off')
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```
blue, green, red = cv2.split(boy_img)
```
```
# Display the blue image
plt.figure(figsize=(8,5))
plt.imshow(blue)
plt.title('Blue image')
plt.axis('off')
plt.show()
```
```
# Display the green image
plt.figure(figsize=(8,5))
plt.imshow(green)
plt.title('Green image')
plt.axis('off')
plt.show()
```
```
# Display the red image
plt.figure(figsize=(8,5))
plt.imshow(red)
plt.title('Red image')
plt.axis('off')
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```
blue, green, red = cv2.split(boy_img)
merged=cv2.merge((blue, green, red))

```
```
# Display the merged (RGB image)
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(merged,cv2.COLOR_BGR2RGB))
plt.title('Merged image')
plt.axis('off')
plt.show()
```


#### 22. Split the image into the H, S, V components & Display the channels.
```
hsv_img=cv2.cvtColor(boy_img,cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv_img)

```
```
# Disply the Hue image
plt.figure(figsize=(8,5))
plt.imshow(h)
plt.title('Hue channel')
plt.axis('off')
plt.show()
```
```
# Disply the Saturation image
plt.figure(figsize=(8,5))
plt.imshow(s)
plt.title('Saturation channel')
plt.axis('off')
plt.show()
```
```
# Display the Value image
plt.figure(figsize=(8,5))
plt.imshow(v)
plt.title('Value channel')
plt.axis('off')
plt.show()
```

#### 23. Merged the H, S, V, displays along with original image.
```
hsv_img=cv2.cvtColor(boy_img,cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv_img)
merge_hsv=cv2.merge((h,s,v))
merge_bgr=cv2.cvtColor(merge_hsv,cv2.COLOR_HSV2BGR)

```
```
# Diaplay the original image
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(boy_img,cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')
plt.show()
```
```
# Display the merged HSV->BGR
plt.figure(figsize=(8,5))
plt.imshow(cv2.cvtColor(merge_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV → BGR")
plt.axis("off")
plt.show()
```

## Output:
- **i)** Read and Display an Image.
<img width="647" height="533" alt="image" src="https://github.com/user-attachments/assets/5539ff9a-6d54-4784-9f2a-29ea606d7f91" />
  
- **ii)** Adjust Image Brightness.
<img width="688" height="535" alt="image" src="https://github.com/user-attachments/assets/c1273d71-508d-4d04-80fe-a446919a56c4" />

- **iii)** Modify Image Contrast.
- <img width="691" height="543" alt="image" src="https://github.com/user-attachments/assets/b70d4d81-b2f6-442f-bc4b-bdbee97ac969" />


## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
