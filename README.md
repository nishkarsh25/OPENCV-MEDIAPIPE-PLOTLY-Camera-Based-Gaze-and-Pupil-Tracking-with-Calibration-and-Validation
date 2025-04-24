# OPENCV-MEDIAPIPE-PLOTLY-Camera-Based-Gaze-and-Pupil-Tracking-with-Calibration-and-Validation

A real-time, webcam-based gaze and pupil tracking system using **OpenCV** and **MediaPipe**, featuring blink detection, gaze direction classification, pupil dilation estimation, and interactive visualizations.

## Introduction

This project implements a **real-time camera-based gaze and pupil tracking system** using **OpenCV**, **MediaPipe**, and other computer vision techniques. It tracks eye movement, estimates pupil dilation, detects blinks, and classifies gaze direction into eight predefined zones.

The system provides a non-invasive way to monitor visual attention and eye behavior without requiring specialized hardware. It includes a calibration mechanism using a red cross moving along a rectangular path on the screen to gather gaze and pupil data across all screen regions.

## Features

### Face and Eye Landmark Detection
- Uses **MediaPipe Face Mesh** to extract 468 facial landmarks.
- Focuses on key eye landmarks to isolate eye regions precisely.

### Real-Time Gaze Direction Estimation
- Tracks both left and right pupils across frames.
- Computes gaze vector based on the displacement of the pupil from the eye center.
- Classifies gaze direction into **8 labeled zones** (e.g., center, top-left, bottom-right).

### Pupil Dilation Measurement
- Detects pupil size (radius) in both eyes using contour-based image processing.
- Computes and stores **average pupil dilation per frame**.
- Useful for studying **cognitive load**, **light response**, and **emotional arousal**.

### Blink Detection (Per-Eye)
- Calculates **Eye Aspect Ratio (EAR)** to detect eye closures.
- Records blinks for the **left**, **right**, or **both eyes** separately.
- Annotates frame with "Left Blink" or "Right Blink" accordingly.

### Calibration Using Moving Red Cross
- Displays a **red cross marker** that moves in a rectangular path across the screen.
- Helps users follow a known path for accurate gaze calibration.
- Used to map gaze data against screen coordinates without hardware calibration tools.

### Data Logging and Visualization
- Records all data including:
  - Gaze vectors (X, Y)
  - Pupil coordinates
  - Pupil size (dilation)
  - Blink events
- Visualizes everything using **Plotly** in 8 interactive graphs:
  - Gaze X over time
  - Gaze Y over time
  - Pupil size over time
  - Left/Right pupil (X, Y) coordinates
  - Blink detection timeline

### Real-Time Frame Annotations
- Displays all results on video frames with:
  - Gaze arrows
  - Pupil centers
  - Text overlays for gaze direction, blink status, and pupil size
  - Live facial feature visualization

### Frame & Data Storage
- Saves all processed frames as `.jpg` images (optional).
- Stores all analytical data for further processing or ML training.

### Optional Extensions (For Future Work)
- Heatmap generation from gaze points
- Blink frequency analytics
- Calibration-free regression using ML
- Audio-visual feedback for blinks or gaze shifts


## Report

You can view the detailed project report [here](https://res.cloudinary.com/drkwwvdoe/image/upload/v1745360048/IEEE_IONI_pwzvkj.pdf)

## Folder Structure

```
📦Calibration_Images
📦captured_frames
📜Code_Pipeline.ipynb
📜Captured_Frames_Analysis.png
📜License

```

## Screenshot/Pipleine/Results

<img src="https://github.com/nishkarsh25/OPENCV-MEDIAPIPE-PLOTLY-Camera-Based-Gaze-and-Pupil-Tracking-with-Calibration-and-Validation/blob/main/Captured_Frames_Analysis.png?raw=true" alt="Screenshot 1" width="1000">

## Tech Stack

This project leverages a combination of cutting-edge computer vision, machine learning, and data visualization tools. Below is a breakdown of the technologies used:

### Computer Vision
- **OpenCV**: For real-time video processing, frame manipulation, pupil detection, contour analysis, and drawing annotations on frames.
- **MediaPipe Face Mesh**: For highly accurate facial landmark detection, especially for eye region tracking.

### Data Visualization
- **Plotly**: Used to create interactive and high-quality plots of gaze direction, pupil size, blink events, and more.

### Eye Tracking & Analysis
- **Custom Algorithms**: For Eye Aspect Ratio (EAR) calculation, blink detection, gaze direction classification, and pupil radius estimation.
- **Gaze Direction Classification**: Maps continuous gaze vectors into 8 discrete screen directions.

### Programming Language
- **Python 3.x**: Core language for all logic, processing, and visualization tasks.

### Supporting Libraries
- `numpy`: For vector math and numerical operations.
- `os`: For file handling and saving frames.
- `math`: Used in EAR and geometric calculations.

### Hardware Requirements
- **Standard Webcam** (no IR or special hardware required)
- Compatible with both **Windows** and **Linux** systems.




## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

## Prerequisites

Before running the pipeline, ensure you have the following installed:

- Python 3.8 or above
- pip (Python package installer)
- Jupyter Notebook or any Python IDE that supports `.ipynb` files


## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/nishkarsh25/OPENCV-MEDIAPIPE-PLOTLY-Camera-Based-Gaze-and-Pupil-Tracking-with-Calibration-and-Validation.git
   ```

2. Navigate to the project branch:

   ```bash
   git checkout <branch-name>
   ```

   Replace `<branch-name>` with the name of the branch you want to checkout.

3. Install Required Dependencies

   Lastest versions of `mediapipe` require `numpy` version 1.26.x for compatibility. To ensure everything works smoothly, install the dependencies with the following commands:

   First, downgrade `numpy`(if necessary):
   ```bash
   python -c "import numpy; print(numpy.__version__)"
   pip install numpy==1.26.4
   ```
   
   ```bash
   pip install opencv-python mediapipe pandas numpy matplotlib plotly scipy
   ```

4. Run the Notebook
   
   Open Code_Pipeline.ipynb using Jupyter Notebook or your preferred environment and run the cells sequentially.
   
   ```bash
   jupyter notebook Code_Pipeline.ipynb
   ```


## Usage

Follow these steps to run the camera-based finger impact detection system:

## Note: 
   - The current images present in the `Calibration_Images` folder were captured using the **repository admin's webcam**. These **must be removed** before proceeding.
   - **Clear all previous images** in the `Calibration_Images` folder before adding new ones. If calibration images were previously taken from a different device, they might not work correctly for your webcam or phone calibration.
   - The **intrinsic and extrinsic properties** of the camera (webcam or phone) are device-specific, meaning the calibration images must be captured from the exact device you plan to use for real-time hand tracking.
   - If you're using **your webcam**, make sure the calibration images are taken from your webcam. If you're using **your phone**, capture the images using your phone's camera.


### Step 1: Capture Chessboard Images for Camera Calibration
1. **Print the Chessboard Pattern**: Print a **11x8 chessboard pattern** (10 internal corners horizontally and 7 internal corners vertically). Ensure that the chessboard is printed on a flat sheet of paper and remains undistorted.
   
2. **Take Pictures from Different Angles**:
   - Position the chessboard in front of your webcam/phone and take **at least 10-15 images**. 
   - Make sure the entire chessboard is clearly visible and flat, but you can hold the chessboard at different angles or distances from the camera.
   
3. **Save the Images**:
   - Save all the captured images in a folder named `Calibration_Images`. 
   - Ensure the images are in **.jpg format** (e.g., `image1.jpg`, `image2.jpg`, etc.).

### Step 2: Place Your Images in the Correct Folder
- Place all the **chessboard calibration images** in the `Calibration_Images` folder. This folder will be used for camera calibration.

### Step 3: Run the Calibration Script
- Run the **camera calibration** script to calibrate your webcam and compute the intrinsic parameters.
- This step uses the images you just captured to determine the camera matrix and distortion coefficients.

### Step 4: Set Up the Webcam
- Make sure your webcam is connected to the system and functional. 
- The program will use the webcam to track hand gestures while playing an instrument.

### Step 5: Start the Gaze Detection Pipeline
- Once the calibration is complete, start the main pipeline by running the Python script to begin the pupil tracking and gaze detection.
- The webcam will open, and it will detect your pupil movements as you move your pupil.
- Ensure your eyes are clearly visible to the webcam and positioned within the camera's frame.

### Step 6: Move Your Pupil

Once the application is running and the red cross appears on the screen, follow these instructions:

- Look at the red cross as it moves across the screen.
- Try to only move your eyes, not your head, to improve tracking accuracy.
- The red cross moves along the border of the screen to help calibrate gaze direction and gather useful data.

### Step 7: Quit the Camera Feed
- Press **`q`** on your keyboard to quit the camera feed once you're done playing.

### Step 8: Video Capture
- After pressing **`q`**, the system will save the frames of the webcam video in a folder named **`captured_frames_IONI`**.
- Each frame will be saved as an image in this folder, allowing you to review the frames later.

### Step 9: Visualize Results
After the tracking is complete, a series of interactive plots will be rendered in your browser to show various tracking results:

- **Gaze Direction over Time**: A plot will display the gaze direction (X and Y coordinates) over the frames, indicating the movement and position of the gaze across time.
- **Pupil Dilation**: A graph will visualize the pupil dilation (size) over time, giving you insights into pupil response during the tracking session.
- **Left and Right Pupil Coordinates**: Separate plots will show the positions of the left and right pupils as they move throughout the frames.
- **Blink Detection Timeline**: This plot will highlight detected blinks, with vertical lines marking the frames where each blink occurred.

These results will be interactive, allowing you to zoom in on specific regions, hover over data points for detailed information, and explore the data in depth.

> The visualization provides a comprehensive analysis of your gaze, pupil behavior, and blink patterns, offering valuable insights from your tracking session.


## Contributing

Contributions to this project are highly appreciated! Whether you discover bugs, have feature requests, or wish to contribute improvements, your input is valuable. Here's how you can contribute:

- **Report Issues:** If you encounter any bugs or issues while using MyCalculatorApp, please open an issue on the GitHub repository. Be sure to provide detailed information about the problem and steps to reproduce it.

- **Submit Pull Requests:** If you have enhancements or fixes to propose, feel free to submit a pull request. Contributions that improve the functionality, usability, or performance of this app are welcomed and encouraged.

Contributions are welcome! If you'd like to contribute to this project, please follow these steps:

1. **Fork the Repository**.
2. **Create a New Branch** (`git checkout -b feature/your-feature-name`).
3. **Make Your Changes**.
4. **Commit Your Changes** (`git commit -am 'Add some feature'`).
5. **Push to the Branch** (`git push origin feature/your-feature-name`).
6. **Create a New Pull Request**.

## License

This project is licensed under the [The 3-Clause BSD License](LICENSE).Feel free to explore, modify, and contribute to this project as you see fit. Your feedback and contributions are greatly appreciated! 🚀✨

## Acknowledgements

This project was developed as part of a research initiative at the **Indian Institute of Technology Hyderabad (IIT-H)**, under the **Department of Biomedical Engineering** and the **Department of Natural Intelligence**.


## Credits

This project makes use of the following tools and libraries:

- [OpenCV](https://opencv.org/) – For real-time computer vision operations and camera calibration.
- [MediaPipe](https://mediapipe.dev/) – For accurate and efficient hand landmark detection.
- [NumPy](https://numpy.org/) – For numerical operations and efficient matrix handling.
- [Pandas](https://pandas.pydata.org/) – For structured data analysis and manipulation.
- [Matplotlib](https://matplotlib.org/) – For static plotting and visual data representation.
- [Plotly](https://plotly.com/) – For interactive, web-based data visualizations.
- [SciPy](https://scipy.org/) – For signal processing and peak detection.

All libraries and frameworks used are open-source and integral to the completion of this project.

### Dataset:
- All the data used in this project, including calibration and hand tracking video frames, was **self-collected** using a **standard chessboard and webcam/phone setup**.

We sincerely thank all contributors, test subjects, and reviewers who helped validate and improve the pipeline.


## Author

- **Nishkarsh Gupta**
  - GitHub: [nishkarsh25](https://github.com/nishkarsh25)
  - Email: bm21btech11016@gmail.com
