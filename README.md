<start_of_image>s```
import cv2
import numpy as np

# Load the image
image = cv2.imread("pebbles.jpg")

# Convert the image to HSV color space
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

# Create a mask for the pebbles
mask = cv2.inRange(hsv, (30, 30, 30), (180, 255, 255))

# Invert the mask
mask = 255 - mask

# Create a new image with the sand
sand = cv2.imread("sand.jpg")

# Resize the sand image to match the size of the mask
sand = cv2.resize(sand, (mask.shape[1], mask.shape[0]))

# Apply the mask to the sand image
masked_sand = cv2.bitwise_and(sand, sand, mask=mask)

# Replace the pebbles with the sand
image[mask > 0] = masked_sand[mask > 0]

# Convert the image back to BGR color space
image = cv2.cvtColor(image, cv2.COLOR_HSV2BGR)

# Save the image
cv2.imwrite("result.jpg", image)
```
![IMG-20240928-WA0009](https://github.com/user-attachments/assets/eae3c765-b444-4017-90d8-714acf164606)
