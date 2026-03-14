# Project Overview

## Project name

**Rehab Motion Assessment System**

## Summary

A camera agnostic rehab motion analysis system that uses RGB video and pose estimation to assess exercise quality and provide feedback.

## Problem statement

Many rehabilitation exercises still rely on in-person guidance, which costs time and human resources. This system aims to support at-home rehabilitation by tracking body motion, assessing exercise quality, and providing feedback.

## Target Users

- Primary users: patients doing at-home rehabilitation
- Secondary users: elderly users doing daily stretching exercises

## Scope of Current Version

### In scope

- Use RGB video from laptop webcam, phone camera, or uploaded video
- Detect body pose with MediaPipe Pose
- Extract body key points and joint-angle features
- Provide basic real-time feedback
- Provide post-session score and mistake summary

### Out of scope

- Azure Kinect / depth-camera input in current version
- Multi-person tracking
- Personalized rehab prescription
- Perfect medical-grade accuracy

## Input Specification

### Current input

- RGB video stream from webcam, or pre-recorded video
- Single person, full body visible
- Person should face camera with minimal occlusion

### Future input

- Depth / 3D camera input, such as Azure Kinect DK

## Output Specification

### Real-time output

- Pose skeleton overlay on video
- Immediate warnings for incorrect movement
- Optional highlight of problematic body region

### Post-session output

- Overall score
- Summary assessment
- List of detected mistakes
- Progress record for future comparison

## Functional Requirements

### FR1. Pose extraction

The system shall extract body keypoints from each video frame using a pose estimation model.

### FR2. Motion representation

The system shall convert raw keypoints into motion features such as joint angles, vectors, and smoothed trajectories.

### FR3. Exercise monitoring

The system shall track the progression of a rehab exercise and detect whether the user is performing the intended movement.

### FR4. Real-time feedback

The system shall provide immediate feedback when major mistakes are detected during the exercise.

### FR5. Session assessment

After the exercise session ends, the system shall generate an overall score and summarize detected mistakes.

### FR6. Progress tracking

The system shall support saving session results for future comparison.

## Non-Functional Requirements

- Reproducibility: the project should be easy to run and demo
- Modularity: input, pose extraction, analysis, feedback, and visualization should be separated
- Interpretability: feedback and scoring should be understandable, not a black box
- Responsiveness: real-time feedback should appear with low delay
- Usability: the interface can be simple, but demo flow should be clear

## System Pipeline

1. Capture RGB video from webcam or uploaded file
2. Run pose estimation to extract body keypoints
3. Smooth the sequence and compute motion features such as angles / vectors
4. Detect exercise progress and movement errors in real time
5. Compare the full sequence with reference samples and generate final assessment

## Algorithm Choices

- Pose estimation: MediaPipe Pose for lightweight body keypoint extraction from RGB video
- Noise reduction: Gaussian smoothing to reduce frame-level noise
- Sequence comparison: DTW for comparing the performed motion with reference samples
- Real-time feedback: rule-based checks on angles, vectors, and motion phases

## MVP Definition

The first version is considered complete if it can:

- Accept webcam or uploaded RGB video
- Track one rehab exercise for a single user
- Extract pose keypoints reliably enough for demo
- Compute key motion features
- Detect at least a few major mistakes in real time
- Generate a post-session score and error summary
- Run in a clean, reproducible codebase with a demo

## Known Limitations

- Current version uses RGB input rather than 3D camera
- Accuracy depends on camera angle, lighting, and occlusion
- Current system works best for a single person fully visible in front of the camera
- Subtle movement mistakes may still be difficult to detect
- Current UI is minimal and demo-focused

## Future Extensions

- Support depth / 3D camera input again
- Support multiple rehab exercises
- Add a more standardized grading system
- Incorporate ML-based assessment models such as regression / classification
- Improve visualization and progress dashboard
