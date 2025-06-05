## Badminton Analytics
**A Computer Vision Project for Shuttle Tracking, Player Detection, and Action Recognition**


## 🎨 Demo

1. YOLO player detection:
![Yolo Demo](https://github.com/user-attachments/assets/6d2f737e-925c-4220-bdf8-6a1e6ce30f1f)

2. TrackNet Model detection:

   ![Tracknet Demo](https://github.com/user-attachments/assets/d764f03d-37e0-471f-8bf5-e754753fb881)


4. Action Recognition Model:
![Action Lstm](https://github.com/user-attachments/assets/85e86c9a-22d7-41d4-ad3e-2ed835d8abeb)


## 📌 Overview  
This project is a comprehensive computer vision system for analyzing badminton matches. It includes:  
1. **Shuttlecock Tracking** - Implements the *TrackNet* deep learning model to predict the position of the shuttlecock.  
2. **Player Detection** - Uses a custom-trained YOLO model to detect and track both players with bounding boxes.  
3. **Action Recognition** - Classifies player actions (3 classes: Block, Serve and Smash) using MediaPipe landmarks and LSTM-based models.
   
---

## 🛠️ Features  
### 1. **Shuttlecock Tracking (TrackNet)**  
   - Predicts the (x,y) position of the shuttlecock in each frame.  
### 2. **Player Detection (YOLOv8 Custom Model)**  
   - Real-time bounding box detection for both players.  
   - Tracks player movement across frames.  
### 3. **Player Action Classification**  
   - Extracts 3D skeletal landmarks using MediaPipe.
   - Generates Heatmap representation of frames.
   - Trained an LSTM model to classify actions into 3 classes (expandable).  

---

## 📊 Results

| Component                | Metric                            |Performance          |
|--------------------------|-----------------------------------|---------------------|
| TrackNet                 | BinaryCrossEntropy Loss           |        0.04211958048|
| YOLO Player              | mAP@0.5                           |                  88%|
| Action LSTM              | Test Accuracy                     |                  87%|

---
## 🚧 Problems/Challenges
### 1. **Slow Inference Speed**
  - **Action LSTM:** Predictions on a 15-second video take ~30s due to sequential processing of MediaPipe landmarks and LSTM computations. This latency limits real-time applicability.
  - **TrackNet:** High computational cost of heatmap generation and frame-by-frame prediction slows down shuttle tracking, especially on longer videos.
### 2. **Ambiguous Temporal Segmentation for Action Recognition**
  - The current pipeline lacks a robust method to identify start and end frames of actions in continuous video streams. This leads to:
    -  **False Positives:** The LSTM misclassifies transitional movements (e.g., player repositioning) as actions.
    -  **Redundant Predictions:** Overlapping sliding windows generate duplicate predictions for the same action.
