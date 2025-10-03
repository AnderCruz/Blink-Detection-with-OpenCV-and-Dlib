# Blink Detection with OpenCV and Dlib

This project uses OpenCV, Dlib, and SciPy to detect facial landmarks and calculate the eye aspect ratio (EAR) in real-time from a video feed. This can be used for applications like blink detection, drowsiness detection, and more.

## Key Features

  * **Facial Landmark Detection:** Utilizes Dlib's pre-trained facial landmark detector to identify key points on the face, including the eyes.
  * **Eye Aspect Ratio (EAR) Calculation:** Computes the EAR for each eye to determine if the eyes are open or closed.
  * **Real-time Video Processing:** Processes video from a webcam or a video file to perform blink detection in real-time.

## Dependencies

  * OpenCV (`cv2`)
  * NumPy
  * Dlib
  * Matplotlib
  * SciPy

## Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/blink-detection.git
    cd blink-detection
    ```

2.  **Install the dependencies using pip:**

    ```bash
    pip install -r requirements.txt
    ```

    *(Note: You will need to create a `requirements.txt` file listing the dependencies mentioned above)*

3.  **Download the Dlib pre-trained model:**
    You will need to download the `shape_predictor_68_face_landmarks.dat` file. You can find this file on the Dlib website. Place it in the project's root directory or specify the path to it in the code.

## Usage

1.  **Run the Jupyter Notebook:**
    Open and run the `OpenVC_Project.ipynb` notebook in a Jupyter environment.

2.  **Modify the video source (optional):**
    The code is set up to use a webcam. If you want to use a video file, you will need to modify the `cv2.VideoCapture()` line to point to your video file.

3.  **Output:**
    The script will display the video feed with the detected facial landmarks and the calculated eye aspect ratio for each eye.

## How it Works

The core of the project is the calculation of the Eye Aspect Ratio (EAR). The EAR is computed using the Euclidean distance between vertical and horizontal eye landmarks. A lower EAR value indicates that the eye is closing or closed. By monitoring the EAR, we can detect blinks.

### Eye Aspect Ratio (EAR)

The core of this project is the real-time calculation of the Eye Aspect Ratio (EAR). This metric provides a single value representing the openness of the eye. The EAR is computed using the Euclidean distances between specific facial landmarks around each eye.

The facial landmarks are indexed as follows:

  * **Left Eye:** 36, 37, 38, 39, 40, 41
  * **Right Eye:** 42, 43, 44, 45, 46, 47

The EAR is calculated using the following formula:

```
EAR = (||p2 - p6|| + ||p3 - p5||) / (2 * ||p1 - p4||)
```

Where p1 through p6 are the 2D facial landmark locations. The numerator of this equation computes the distance between the vertical eye landmarks, while the denominator computes the distance between the horizontal eye landmarks.

### Blink Detection Logic

A blink is detected by monitoring the EAR value over time. When the eye is open, the EAR will be relatively constant. When a blink occurs, the EAR value will rapidly drop towards zero.

The script establishes a minimum EAR threshold. If the current EAR drops below this threshold, it is considered a blink.

## Code Structure

The Jupyter Notebook contains several key functions:

  * **`eye_aspect_ratio(eye)`:** This function takes the coordinates of the eye landmarks as input and returns the calculated EAR.
  * **`anotar_marcos_casca_convexa(imagem, marcos)`:** This function draws the convex hull around the detected facial landmarks, visualizing the detected points on the video feed.

## Potential Applications (Expanded)

This blink detection technology has a wide range of potential applications, including:

  * **Driver Drowsiness Detection:** By monitoring the frequency and duration of blinks, a system can alert a driver who is becoming drowsy.
  * **Attention Monitoring:** In educational or professional settings, this can be used to gauge a person's level of attention to a task or presentation.
  * **Assistive Technology:** For individuals with severe motor disabilities, blinks can be used as a voluntary signal to control a computer or other devices.
  * **Human-Computer Interaction:** Blinks could be incorporated as a form of input for games or other interactive applications.

## Customization

To adapt the blink detection for different individuals or environments, you can adjust the following parameters in the code:

  * **EAR Thresholds (`min_olho_esq`, `min_olho_dir`):** These values determine the minimum EAR before a blink is registered. You may need to fine-tune these thresholds for different people, as the EAR can vary based on facial structure. Lighting conditions can also affect the detection, so adjustments may be necessary.
