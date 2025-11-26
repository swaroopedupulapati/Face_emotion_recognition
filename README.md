# 😄 Real-Time Face Emotion Recognition Web App

> This project implements a real-time emotion detection system using a webcam feed, deploying the output to a web browser via a **Flask** application. It leverages the **`fer` (Face Emotion Recognition)** library, which utilizes deep learning models to identify human emotions.

## ✨ Features

  * **Real-Time Processing:** Captures video from the webcam and processes frames continuously.
  * **Emotion Detection:** Utilizes the `fer` library's pre-trained model to detect and classify up to **7 core emotions** (e.g., happy, sad, angry, neutral).
  * **Visual Output:** Draws a **bounding box** around detected faces and displays the **dominant emotion** directly on the video feed.
  * **Web Streaming:** Uses **Flask**'s `Response` object with `multipart/x-mixed-replace` to stream the processed video frames efficiently to the client browser.

-----

## ⚙️ Technology Stack

| Category | Tool / Library | Purpose |
| :--- | :--- | :--- |
| **Web Framework** | `Flask` | Serves the web application and handles video streaming routes. |
| **Computer Vision** | `cv2` (OpenCV) | Captures video from the webcam and handles image manipulation (drawing boxes, text). |
| **Emotion Detection** | `fer` | Core library for deep learning-based face detection and emotion classification. |

-----

## 💻 Getting Started

### Prerequisites

You must have **Python 3.x** installed. A functioning **webcam** is required for the application to capture video.

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [YOUR_REPOSITORY_URL]
    cd face-emotion-recognition
    ```
2.  **Install the required libraries:**
    The `fer` library has several dependencies, including TensorFlow/Keras and OpenCV.
    ```bash
    pip install Flask opencv-python fer
    ```

### Project Structure

Ensure your project directory contains the following two files:

```
face-emotion-recognition/
├── app.py                      <-- Your Python script (Flask app)
└── templates/
    └── index.html              <-- The frontend HTML file (see below)
```

**`index.html` (Example)**

You need a basic HTML template in the `templates/` folder to display the video feed:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Real-Time Emotion Recognition</title>
</head>
<body>
    <h1>Live Emotion Stream</h1>
    <img src="{{ url_for('video_feed') }}" width="640" height="480">
</body>
</html>
```

-----

## ▶️ Execution

1.  **Run the Flask application:**
    ```bash
    python app.py
    ```
2.  The application will start running (usually on `http://127.0.0.1:5000/`).
3.  Open your web browser and navigate to the displayed URL. You should see the live webcam feed with bounding boxes and predicted emotions over any detected face.

## 🛠️ Code Breakdown

### `generate_frames()`

  * This function is a **Python generator**. It reads frames from the webcam (`cv2.VideoCapture(0)`).
  * It calls `detector.detect_emotions(frame)` to get face coordinates and emotion scores.
  * It finds the **dominant emotion** (`max_emotion`) and draws the result on the frame.
  * The frame is encoded to **JPEG** and yielded in a format required for **MJPEG streaming** (`multipart/x-mixed-replace`).

### `video_feed()`

  * This Flask route returns a **Streamed Response**.
  * It calls `generate_frames()` and sets the `mimetype` to `multipart/x-mixed-replace; boundary=frame`, which tells the browser to treat the incoming data as a continuous stream of JPEG images.

-----

## 🤝 Contribution

Feel free to fork the repository and contribute improvements, such as:

  * Adding emotion logging or data storage.
  * Improving the frontend layout.
  * Implementing face blurring for privacy.
