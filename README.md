# BICEPS_CURLER_COUNTER

The **BICEPS_CURLER_COUNTER** is a fitness tool designed to help gym enthusiasts estimate their biceps curling pose and track the number of repetitions (reps) they are performing. By analyzing the angle of the bicep during the curling motion, the system accurately counts the reps in real-time through a camera feed or video input.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Keypoints and Angle Calculation](#keypoints-and-angle-calculation)
- [Tracking Reps](#tracking-reps)
- [Results](#results)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/codeflamer/POSE-ESTIMATION.git
   cd POSE-ESTIMATION/BICEPS CURLER APP
   ```

2. Install the required dependencies:
   It is preferabele to run in a virtual environment making use of environments like conda or venv.

   Requirements:

   - protobuf
   - mediapipe
   - opencv-python
   - numpy

   ```bash
   pip install protobuf==4.25.5 mediapipe opencv-python numpy
   ```

## Usage

After installing the required libraries, you can run the program to start counting bicep curl repetitions from a camera feed or video.

```bash
jupyter notebook
```

You can run this from the command line and execute the cells in the BICEPS_CURLER_COUNTER.ipnb

The application will track your bicep curls and display the current count of repetitions based on your pose.

## Keypoints for Angle Calculation

In order to correctly estimate the number of repetitions, the system uses **MediaPipe** to detect keypoints on the body, particularly focusing on the elbow, shoulder, and wrist. These keypoints are crucial for measuring the angle of the bicep during a curl.

To measure the angle of the bicep:

- The angle is calculated using the elbow as the vertex and the shoulder and wrist as the defining points.
  <img src="./BICEPS%20CURLER%20APP/keypoints.png" alt="Keypoints from Mediapipe" height="400" width=400/>
  ![Body Keypoints and Angle Calculation](/BICEPS%20CURLER%20APP/angle_calculation.png)

This angle is then used to determine the stage of the curl, which in turn tracks the reps:

```python
if angle > 140:
    stage = "down"
if angle < 45 and stage == "down":
    counter += 1
    stage = "up"
```

## Tracking Reps

The system follows the below logic for counting repetitions:

1. **Down Stage**: If the arm is fully extended, with the elbow angle greater than 140 degrees, the stage is set to "down."
2. **Up Stage**: As the bicep contracts and the elbow angle decreases below 45 degrees, a rep is counted, and the stage is updated to "up."

The cycle repeats to accurately count each bicep curl during the exercise.

## Results

Here’s an example of the output from the system, where the biceps curl repetitions are counted in real-time from a camera feed:

![Biceps Curl Counter Result](./BICEPS%20CURLER%20APP/results/CurlerCounter.gif)

The current rep count and stage (up or down) are displayed on the video feed for real-time feedback.
