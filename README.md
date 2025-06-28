# Player Detection and Re-Identification using YOLOv11 and DeepSORT
# 1. Introduction
In this project, we address the problem of player tracking and re-identification in sports videos. The objective is to detect players in a given video, assign each a unique ID, and consistently maintain that ID even if the player temporarily leaves and re-enters the scene. This is particularly useful for sports analytics, performance monitoring, and automated highlights generation.

To achieve this, we utilize a custom-trained YOLOv11 model for object detection and DeepSORT for multi-object tracking. The final system simulates real-time player detection and tracking over a 15-second input video.

# 2. Methodology
# 2.1 Object Detection using YOLOv11
We use the YOLOv11 model (You Only Look Once, version 11) trained specifically for detecting players in sports footage.

YOLOv11 is a fast and accurate object detector that predicts bounding boxes and class probabilities directly from full images in a single evaluation.

For this task, we use a custom model (best.pt) trained only to recognize players, making it more precise in sports environments.

# 2.2 Tracking using DeepSORT
DeepSORT (Simple Online and Realtime Tracking with a Deep Association Metric) is used to track objects between frames and assign persistent identities.

It combines motion-based Kalman filtering with deep appearance descriptors, enabling re-identification of players after occlusions or exits.

The tracker uses features like bounding box coordinates, motion vectors, and visual similarity to maintain consistent player IDs.

# 3. Filtering and Post-Processing
To improve detection quality and reduce false positives, we apply:

Confidence Thresholding: Detections with confidence below 0.5 are discarded.

Size Filtering: Bounding boxes that are either too small or too large are likely false positives and ignored.

Aspect Ratio Filtering: Ensures that only boxes with realistic human-like proportions are kept.

Bounding Box Clipping: Bounding boxes are clipped to the frame dimensions to prevent drawing outside the image.

# 4. Output Generation
The system produces two types of output:

Annotated Video (output_tracked.mp4):

Displays each detected player with a bounding box and their unique ID over time.

Tracking Log (tracking_log.csv):

A CSV file that stores the frame number, player ID, and bounding box coordinates (x1, y1, x2, y2).

This log can be used for downstream analysis like player trajectories, speed estimation, and tactical heatmaps.

# 5. Results
The system was tested on a 15-second, 720p sports video.

It was able to consistently detect and track players with minimal ID switches or false detections.

Bounding boxes were drawn around each player, and their IDs remained consistent throughout the clip.

# 6. Conclusion
This project successfully demonstrates the integration of a custom-trained YOLOv11 model with the DeepSORT tracker for real-time player detection and tracking. The system handles occlusions and re-identifications robustly, producing accurate and consistent results suitable for further sports analytics tasks.

Future work may include:

Ball tracking

Multi-camera ID fusion

Player behavior recognition using pose estimation or action classification
