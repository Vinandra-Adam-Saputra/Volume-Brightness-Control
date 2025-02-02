# Hand Gesture Volume and Brightness Control

## Overview
This application enables contactless control of your computer's system volume and screen brightness using hand gestures captured through your webcam. It utilizes computer vision and hand tracking technology to interpret hand movements and convert them into system control commands.

## Features
- **Dual Hand Control**: 
  - Left hand controls screen brightness
  - Right hand controls system volume
- **Real-time Processing**: Instant response to hand movements
- **Visual Feedback**: On-screen display of hand tracking and gesture lines
- **Natural Gesture Interface**: Control through intuitive pinch movements

## Requirements

### Hardware
- Computer cam / Webcam (optional)
- Computer with audio output capabilities
- Display with adjustable brightness

### Software Dependencies
```bash
pip install opencv-python
pip install mediapipe
pip install numpy
pip install comtypes
pip install pycaw
pip install screen-brightness-control
```

## Installation Steps
1. Install all required dependencies using pip
2. Download the `volume_brightness_control.py` script
3. Ensure your webcam is connected and functioning
4. Run the script using Python 3.x

## Usage Instructions

### Starting the Application
1. Open terminal/command prompt
2. Navigate to the script directory
3. Run: `python volume_brightness_control.py`

### Controlling Volume (Right Hand)
1. Show your right hand to the camera
2. Pinch your thumb and index finger together
3. Adjust the distance between fingers:
   - Increase distance → Increase volume
   - Decrease distance → Decrease volume
   - Range: 15-200 pixels maps to system volume range

### Controlling Brightness (Left Hand)
1. Show your left hand to the camera
2. Pinch your thumb and index finger together
3. Adjust the distance between fingers:
   - Increase distance → Increase brightness
   - Decrease distance → Decrease brightness
   - Range: 15-200 pixels maps to 0-100% brightness

### Exiting the Application
- Press 'q' to quit the application

## Technical Details

### Hand Detection
- Uses MediaPipe Hands for hand landmark detection
- Minimum detection confidence: 75%
- Tracks 21 3D hand landmarks per hand
- Distinguishes between left and right hands

### Volume Control Implementation
```python
# Volume range mapping
volMin, volMax = volume.GetVolumeRange()[:2]
# Distance to volume conversion
vol = np.interp(length, [15, 200], [volMin, volMax])
```

### Brightness Control Implementation
```python
# Brightness range mapping
bright = np.interp(length, [15, 200], [0, 100])
```

### Key Components
1. **Video Capture**: OpenCV VideoCapture
2. **Hand Processing**:
   - MediaPipe hand detection
   - Landmark extraction
   - Hand side classification
3. **Gesture Measurement**:
   - Euclidean distance calculation between landmarks
   - Linear interpolation for control mapping
4. **System Control**:
   - PyCaw for audio control
   - screen_brightness_control for display brightness

## Customization

### Adjusting Sensitivity
Modify the interpolation ranges in the code:
```python
# For brightness (default)
bright = np.interp(length, [15, 200], [0, 100])
# For volume (default)
vol = np.interp(length, [15, 200], [volMin, volMax])
```

### Screenshoot
![WhatsApp Image 2025-02-02 at 12 19 50](https://github.com/user-attachments/assets/0439f5be-4260-4569-82cd-f604779e901d)


## Contributing

To contribute to this project:
1. Fork the repository
2. Create a feature branch
3. Implement your changes
4. Submit a pull request

## License
This project is released under the [MIT License](LICENSE)

## Acknowledgments
- Project By: [Curious Programmer](https://codewithcurious.com/)

