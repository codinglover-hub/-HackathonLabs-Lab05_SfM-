# Structure-from-Motion (SfM) / NeRF Project

## Overview
This project implements a basic Structure-from-Motion (SfM) and Neural Radiance Fields (NeRF) pipeline.  
It extracts features, reconstructs 3D points, and visualizes the scene.

## Reflection Questions & Answers

**Q1:** Why do SIFT features remain stable across multiple images?  
**A1:** Because SIFT features are invariant to scale, rotation, and partially to illumination changes, making them robust across images.  

**Q2:** What parameters or unknowns increase when cameras are uncalibrated?  
**A2:** Intrinsic camera parameters (focal length, principal point) and distortion coefficients increase as unknowns.  

**Q3:** What does bundle adjustment refine after triangulation?  
**A3:** It refines camera poses and 3D point positions to minimize reprojection error.  

**Q4:** What is the real-world trade-off between accuracy and runtime in SfM?  
**A4:** Higher accuracy requires more computation and runtime; faster methods sacrifice precision for speed.

## Results
 
1) Feature Detection
Top 100 SIFT keypoints detected per image.
Keypoints visualized: feature_keypoints.png

Observation: Keypoints cover textured areas densely, ensuring robust matching.

3) Feature Matching
Matched using BFMatcher with crossCheck=True.
Visual output: output_match.jpg

Observation: Increasing ratio threshold reduces false matches but may remove valid ones.

5) Geometry Estimation
Fundamental Matrix (F) computed using RANSAC.
Inlier matches: 85 / 100

Observation: Smaller RANSAC thresholds increase accuracy but reduce inliers.

7) Pose Estimation
Essential Matrix (E) computed assuming intrinsic matrix K.
Rotation (R) and translation (t) recovered: pose.txt

Translation vector direction: Indicates the relative motion between cameras along the 3-D scene.

9) 3-D Reconstruction
Points triangulated using cv2.triangulatePoints().
3-D visualization: reconstruction.png

Observation: Flattened reconstruction indicates small baseline or calibration errors.

11) Creative Visualization (Bonus)

In this experiment, we tested different feature detectors—SIFT, ORB, and AKAZE—to compare their effect on 3-D reconstruction.

SIFT produced the most stable and accurate point matches across images due to its invariance to scale and rotation.

ORB and AKAZE were faster but yielded fewer and less precise matches, slightly reducing reconstruction quality.

This demonstrates the trade-off between accuracy and runtime, helping choose a detector based on task priorities.
