# Week 4

<span style="opacity: 0.5;">10/09/2023 - 10/13/2023</span>

Unfortunately, I caught a terrible cold or flu at the end of last week that had me in bed and unable to look at a screen. I stayed home away from the Recurse Center hub and focused on resting and reading.

## Digital finger painting

[GitHub Repo](https://github.com/sshovkov/finger-painting-hand-recognition-model)

When I started recovering from my cold, I jumped back into playing with Google's MediaPipe library and the [hand-tracking model from last week](https://github.com/sshovkov/recurse-center-journal/blob/main/Week3.md#experimenting-with-googles-mediapipe). I expanded on my initial implementation by creating an interactive real-time finger painting application.

![](assets/week4/finger_painting_small_file.gif)

**Controls:**

- Right hand: Use your right index finger to draw on the screen.
- Left hand: Raise and hold your left hand to stop drawing.

**How it works:**

The code utilizes the MediaPipe library for hand tracking and OpenCV for image processing. When the program is executed, it initializes a hand-tracking model using the MediaPipe library, specifically the Hands module.

The hand landmarks detected include the position of the fingertips and other key points on the hand. If a hand is detected and painting mode is enabled (toggled with the space bar), the program identifies the handedness. If the left hand is detected, drawing is paused; otherwise, drawing is enabled.

When drawing is enabled, the program first draws red circles on all detected landmarks for hand-tracking visualization. To create a responsive, and natural drawing interaction, the program tracks the position of the right hand's index fingertip (landmark 8) in the current frame and compares it with the position in the previous frame, computing the difference in X and Y coordinates. The code implements a simple linear interpolation algorithm to estimate the positions of the index fingertip between consecutive frames, resulting in a  visually appealing, responsive, and continuous drawing experience. 

The drawn lines are superimposed onto an existing canvas. The canvas is represented as a NumPy array with the same dimensions as the video frame. The drawn lines are blended with the canvas using the `cv2.addWeighted()` function, creating a persistence effect and allowing for continuous drawing without clearing the canvas.
