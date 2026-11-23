# HOUGH-TRANSFORM

## NAME : SADHANA S
## REG.NO : 212224230234

## Aim 

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

## Learning Objective

Understand each stage of image processing

Learn how to build a complete computer vision pipeline

Practice writing code in guided sections

## Software Used

Anaconda – Python 3.7

Jupyter Notebook / VS Code

OpenCV (cv2)

NumPy

Matplotlib

## Program

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Load the image using imread() from cv2 module
image = cv2.imread(r"C:\Users\admin\Downloads\mypic.jpeg")

# Step 3: Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Input image and grayscale image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Convert image to RGB for displaying
plt.title("Input Image")
plt.axis('off')

plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')

# Step 4: Using Canny operator from cv2, detect the edges of the image
edges = cv2.Canny(gray_image, 50, 150)  # Canny edge detection with threshold values 50 and 150

# Canny Edge Detector output
plt.imshow(edges, cmap='gray')
plt.title("Canny Edge Detector")
plt.axis('off')

# Step 5: Using the HoughLinesP(), detect line coordinates for every point in the image
# The parameters of HoughLinesP are: image, resolution, threshold, minLineLength, maxLineGap
lines = cv2.HoughLinesP(edges, 1, np.pi / 180, 100, minLineLength=50, maxLineGap=10)

# Step 6: Using a for loop, draw the lines on the original image using the detected coordinates
# The lines variable contains the endpoints of the detected lines
for line in lines:
    x1, y1, x2, y2 = line  # Unpacking the line coordinates
    cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 2)  # Draw green lines with thickness of 2

# Display the result of Hough Transform (Image with lines)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Image with lines drawn
plt.title("Result of Hough Transform")
plt.axis('off')
```





## Output

## Original image

<img width="322" height="570" alt="image" src="https://github.com/user-attachments/assets/72612a7b-9166-479c-80fc-06e24f67510d" />


## Grayscale image

<img width="371" height="577" alt="image" src="https://github.com/user-attachments/assets/840fc94b-a87a-4313-91f9-2a53cde85bd6" />


## Canny Edge Detector image

<img width="346" height="564" alt="image" src="https://github.com/user-attachments/assets/8147c610-4a78-483a-9354-f6faaa707d14" />

## Hough Transform image

<img width="392" height="561" alt="image" src="https://github.com/user-attachments/assets/9d43b593-0ade-4b2d-8d03-8a829bfe7a07" />




## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.
