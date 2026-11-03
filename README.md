#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
img = cv2.imread("lane.png")

if img is None:
    raise FileNotFoundError("Image not found! Check the image path.")

print("Image loaded successfully!")
```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```

---

###  Step 5: Thresholding

```python
threshold = cv2.threshold(
    gray, 150, 255, cv2.THRESH_BINARY
)[1]

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```

---

###  Step 6: Region of Interest (ROI)

```python
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (int(width * 0.05), height),
    (int(width * 0.95), height),
    (int(width * 0.60), int(height * 0.55)),
    (int(width * 0.40), int(height * 0.55))
]], dtype=np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)

plt.imshow(roi, cmap="gray")
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()
```

---

### Step 7: Edge Detection (Canny)

```python
edges = cv2.Canny(roi, 50, 150)

plt.imshow(edges, cmap="gray")
plt.title("Edge Detected Image")
plt.axis("off")
plt.show()
```

---

###  Step 8: Gaussian Blur

```python
blur = cv2.GaussianBlur(edges, (5, 5), 0)

plt.imshow(blur, cmap="gray")
plt.title("Smoothed Image")
plt.axis("off")
plt.show()
```

---

###  Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi / 180,
    30,
    minLineLength=30,
    maxLineGap=100
)
```

---

### Step 10: Lane Detection Logic

```python
left_lines = []
right_lines = []

if lines is not None:

    for line in lines:
        x1, y1, x2, y2 = line[0]

        if x2 == x1:
            continue

        slope = (y2 - y1) / (x2 - x1)

        if abs(slope) < 0.4:
            continue

        if slope < 0:
            left_lines.append((x1, y1, x2, y2))
        else:
            right_lines.append((x1, y1, x2, y2))
```

---

##  Expected Output

* Original image
  
<img width="570" height="466" alt="image" src="https://github.com/user-attachments/assets/b81c18f3-4015-466c-a203-1ae25026bb11" />

* Grayscale image

  <img width="617" height="485" alt="image" src="https://github.com/user-attachments/assets/a6c0d79a-a2ab-4e53-8ff6-f981a2802735" />

* Thresholded image

  <img width="662" height="517" alt="image" src="https://github.com/user-attachments/assets/5b81ba78-cf2c-46a7-8428-71ec621d5c14" />

* ROI masked image

  <img width="697" height="517" alt="image" src="https://github.com/user-attachments/assets/8c28ae76-18cb-4df3-af71-1553c131f8b4" />

* Edge detected image

  <img width="627" height="522" alt="image" src="https://github.com/user-attachments/assets/a0aaf2af-694d-40a3-bf2d-bb8f93c68825" />

* Smoothed image

  <img width="700" height="530" alt="image" src="https://github.com/user-attachments/assets/47256297-fe9d-48f9-a40e-f2333415791c" />

* Final lane detection output

  <img width="782" height="637" alt="image" src="https://github.com/user-attachments/assets/72078bdc-aeee-409f-bc24-7d5b0a8a29bf" />



---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---

##  Developed By

* **Name: Hemapriya P** 
* **Register No: 212225040126**
