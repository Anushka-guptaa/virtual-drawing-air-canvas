Project Title: Air Canvas – Real-Time Virtual Drawing Using Hand Motion

Description:
------------
This project allows users to draw in the air using a colored object (like a pink cap) by tracking its movement with a webcam. OpenCV processes 
the video stream, detects the colored object using HSV masking, and maps it to a virtual canvas for drawing in real-time.

Tools and Libraries:
--------------------
- Python 3.x
- OpenCV
- NumPy

How to Run:
-----------
1. Install Python 3
2. Open Terminal or Command Prompt in this folder
3. Install required packages:
   pip install numpy opencv-python

4. Run the script:
   python air_canvas.py

5. Tune HSV sliders in the 'Color detectors' window to match your object.
6. Start drawing in the 'Paint' window using your colored object.
7. Hover over color boxes to switch colors.
8. Hover over 'CLEAR' to clear the canvas.
9. Press 'q' to exit the program.

Sample Code Snippets:
---------------------

# Capture video and convert to HSV
cap = cv2.VideoCapture(0)
ret, frame = cap.read()
frame = cv2.flip(frame, 1)
hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

# Define HSV range from trackbars
lower_hsv = np.array([l_hue, l_saturation, l_value])
upper_hsv = np.array([u_hue, u_saturation, u_value])
mask = cv2.inRange(hsv, lower_hsv, upper_hsv)

# Find and track contours
contours, _ = cv2.findContours(mask.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
if len(contours) > 0:
    cnt = sorted(contours, key=cv2.contourArea, reverse=True)[0]
    ((x, y), radius) = cv2.minEnclosingCircle(cnt)
    M = cv2.moments(cnt)
    center = (int(M["m10"] / M["m00"]), int(M["m01"] / M["m00"]))

# Draw lines on canvas
cv2.line(paintWindow, prev_point, center, colors[colorIndex], 2)

HSV Example for Pink Object:
----------------------------
Lower HSV: [145, 100, 100]  
Upper HSV: [170, 255, 255]  

External Resources:
-------------------
- No datasets used
- Real-time webcam input 

Created By:
Anushka Gupta  

