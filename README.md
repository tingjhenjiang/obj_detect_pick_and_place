# obj_detect_pick_and_place
With a phone, PC, conveyor, air compressor, step motor, PLC, do pick and place.

# 原圖與標註（物件偵測） Original image and annotations（object detection）
![originalimage](https://github.com/user-attachments/assets/fdf13b5f-bb10-4415-afdb-17134ad4b081)
![image](https://github.com/user-attachments/assets/0d30b725-68b6-4cc7-b786-431530f94720)

# 物件偵測模型訓練 Yolov7 object detection model training
![results](https://github.com/user-attachments/assets/188062dc-4a67-4f22-ad26-7482317c26fa)


# 問題 Problem definition
由於相機相機架設角度，使得吸嘴的中心位置與積木的中心位置即便落在同一座標上從影像上看來也有不同。
Even a building block is right under the nozzle and share the same centroid in fact, the centroids are different from camera's perspective. 

# 解方 Solutions

## Locate the boundary of conveyor

contour detection (OpenCV findContours):
![contours](https://github.com/user-attachments/assets/95a9c7d8-2022-4a2b-972f-399a308422c4)

polygon approximation (OpenCV approxPolyDP):
![polylines](https://github.com/user-attachments/assets/0e11c278-3874-4f7e-8c54-397ece75e07b)

get the longest edges whose slope > 1 and surrounding the conveyor to enable perspective transformation:
![correctboundary](https://github.com/user-attachments/assets/bf2f7e9b-1518-4b6e-8678-35a58a38d4e9)

## Apply transformation

apply perspective transformation (OpenCV getPerspectiveTransform warpPerspective):
![perspectiveTransformation](https://github.com/user-attachments/assets/498c69eb-6e3d-44fd-8242-bdea85b1bb50)
