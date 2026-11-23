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

## Step 1: Import Libraries
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

## Step 2: Read the Image
```
image = cv2.imread(r"C:\Users\admin\Downloads\mypic.jpeg")
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```

## Step 3: Convert to Grayscale
```
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

## Step 4: Display Images
```
plt.figure(figsize=(10,5))
plt.subplot(1,2,1); plt.imshow(image_rgb); plt.title("Original")
plt.subplot(1,2,2); plt.imshow(gray, cmap='gray'); plt.title("Grayscale")
plt.show()
```

## Step 5: Thresholding
```
threshold = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)[1]
plt.imshow(threshold, cmap='gray')
plt.title("Threshold")
plt.show()
```

## Step 6: Region of Interest (ROI)
```
roi_vertices = np.array([[[100,540],[900,540],[515,320],[450,320]]])
mask = np.zeros_like(threshold)
cv2.fillPoly(mask, roi_vertices, 255)
roi = cv2.bitwise_and(threshold, mask)

plt.figure(figsize=(15,5))
for i, (img, title) in enumerate([(threshold,"Threshold"),(mask,"Mask"),(roi,"ROI")]):
    plt.subplot(1,3,i+1); plt.imshow(img,cmap='gray'); plt.title(title)
plt.show()
```

## Step 7: Edge Detection (Canny)
```
edges = cv2.Canny(roi, 50, 150)
plt.imshow(edges, cmap='gray')
plt.title("Edges")
plt.show()
```

## Step 8: Gaussian Blur
```
blurred = cv2.GaussianBlur(edges, (5,5), 0)
plt.imshow(blurred, cmap='gray')
plt.title("Smoothed Image")
plt.show()
```

## Step 9: Hough Transform
```
lines = cv2.HoughLinesP(blurred, 1, np.pi/180, 50, minLineLength=50, maxLineGap=100)
line_image = image_rgb.copy()

if lines is not None:
    for x1,y1,x2,y2 in np.array(lines).reshape(-1,4):
        cv2.line(line_image, (x1,y1), (x2,y2), (255,0,0), 3)

plt.imshow(line_image)
plt.title("Detected Lines")
plt.show()
```

## Step 10: Lane Detection Logic
```
lane = np.zeros_like(image_rgb)
h, w = image.shape[:2]

if lines is not None:
    left, right = [], []

    for x1,y1,x2,y2 in np.array(lines).reshape(-1,4):
        if x2 != x1:
            slope = (y2-y1)/(x2-x1)
            (left if slope < 0 else right).append((x1,y1,x2,y2))

    for group in [left, right]:
        if group:
            p = np.array(group)
            fit = np.polyfit(np.r_[p[:,1],p[:,3]], np.r_[p[:,0],p[:,2]], 1)
            cv2.line(lane, (int(np.polyval(fit,h)),h),
                     (int(np.polyval(fit,h*0.6)),int(h*0.6)), (0,255,0), 5)

final_output = cv2.addWeighted(image_rgb, 0.8, lane, 1, 0)

plt.imshow(final_output)
plt.title("Final Lane Detection")
plt.axis("off")
plt.show()
```

## Output

## Original image

<img width="435" height="576" alt="image" src="https://github.com/user-attachments/assets/4937e668-3739-4d4b-a444-16bad1b30f22" />

## Grayscale image

<img width="473" height="579" alt="image" src="https://github.com/user-attachments/assets/54c90160-e780-4fcb-a11f-9bf42bd007d9" />


## Threshold image

<img width="382" height="547" alt="image" src="https://github.com/user-attachments/assets/ddce40af-1398-4a71-b5bd-c52f43d870c0" />

## ROI masked image

<img width="1253" height="527" alt="image" src="https://github.com/user-attachments/assets/2e0b597c-fb56-4157-a3f3-167e6a125386" />

## Edge detected image

<img width="384" height="566" alt="image" src="https://github.com/user-attachments/assets/ab7b706d-baac-4052-8974-6c07a0177550" />

## Smoothed image

<img width="444" height="553" alt="image" src="https://github.com/user-attachments/assets/c57cd4aa-d84e-4d24-bcbc-3af09d205f5a" />

## Detected lines

<img width="402" height="544" alt="image" src="https://github.com/user-attachments/assets/1f204600-63bf-4c14-98b2-9a96dea4b8a8" />

## Final lane detection output

<img width="311" height="532" alt="image" src="https://github.com/user-attachments/assets/0c28ac2f-4fe8-453e-a3d7-5aff97592495" />

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.
