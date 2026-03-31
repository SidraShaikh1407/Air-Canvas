# Air Canvas ✋🎨

Draw in the air using just your webcam and a colored object - no mouse, no touchscreen required.

## How it works

Air Canvas uses your webcam to track a specific colored object (by default, a red/pink object) in real time. As you move the object in front of the camera, OpenCV detects it and draws lines on a virtual canvas overlay, mapping your hand's trajectory into digital art.

## Features

- Real-time color tracking via HSV color segmentation
- Draw on a transparent canvas overlaid on the live video feed
- Switch between 5 colors: **Blue, Violet, Green, Red, Yellow**
- Clear the canvas instantly with the on-screen button
- Color selection buttons displayed directly in the video frame

## Requirements

- Python 3.x
- OpenCV (`cv2`)
- NumPy

Install dependencies:
```bash
pip install opencv-python numpy
```

## Running the project

```bash
python air_canvas.py
```

A webcam window will open. Hold a **red or pink colored object** in front of the camera to start drawing.

Press **`q`** to quit.

## Controls

All controls are displayed as buttons in the top bar of the video window:

| Button | Action |
|---|---|
| CLEAR ALL | Wipes the canvas |
| BLUE | Switches drawing color to blue |
| VIOLET | Switches drawing color to violet |
| GREEN | Switches drawing color to green |
| RED | Switches drawing color to red |
| YELLOW | Switches drawing color to yellow |

Move your tracked object into a button's region (top 65px of the frame) to activate it.

## Customizing the tracked color

The default tracking target is a red/pink object, defined by this HSV range in `air_canvas.py`:

```python
lower_bound = np.array([170, 120, 70])
upper_bound = np.array([180, 255, 255])
```

To track a different color, update these values. You can use an HSV color picker or OpenCV's `cv2.inRange` docs to find the right range for your object.

## How drawing works

1. The script captures each webcam frame and flips it horizontally (mirror mode).
2. The frame is converted to HSV color space and masked to isolate the tracked color.
3. The largest contour in the mask is identified as the "pen tip."
4. A line is drawn on the canvas between the contour's center point in consecutive frames.
5. The canvas is blended back onto the live video feed using bitwise operations.

## Project structure

```
air_canvas.py   # Main script — all logic lives here
README.md
```

## Credits

Built by **Sidra Shaikh**, based on the Air Canvas tutorial by [TechVidvan](https://techvidvan.com).