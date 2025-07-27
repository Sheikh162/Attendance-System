# Face Recognition Attendance System

A Python-based attendance system leveraging real-time face recognition with dlib and OpenCV, featuring a Tkinter GUI for face registration and a Flask web interface for attendance lookup.

---

## Features

- **Face Registration:** Register new users via webcam using a Tkinter GUI. Images are stored in `data/data_faces_from_camera/`.
- **Feature Extraction:** Extracts 128D facial features using dlib's ResNet model and stores them in `data/features_all.csv`.
- **Real-Time Recognition & Attendance:** Recognizes faces from webcam input, marks attendance in an SQLite database (`attendance.db`), and prevents duplicate entries per day.
- **Web Interface:** Flask app to view attendance records by date, rendered with Bootstrap for a clean UI.

---

## Project Structure

```
Attendance/
│
├── app.py                        # Flask web server for attendance lookup
├── attendance_taker.py           # Main script for real-time face recognition and attendance marking
├── features_extraction_to_csv.py # Script to extract features from registered face images
├── get_faces_from_camera_tkinter.py # GUI for registering new faces via webcam
├── data/
│   ├── data_dlib/                # Pre-trained dlib models (not for commit)
│   ├── data_faces_from_camera/   # Registered face images (not for commit)
│   └── features_all.csv          # Extracted face features (not for commit)
├── templates/
│   └── index.html                # Web UI template
├── requirements.txt              # Python dependencies
└── venv/                         # Virtual environment (not for commit)
```

---

## 📦 Data & Model Files

This repository does **not** include the `data/` folder (models, face images, features) due to size and privacy.

**To set up:**
1. **Download dlib models**  
   - [shape_predictor_68_face_landmarks.dat](http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2)  
   - [dlib_face_recognition_resnet_model_v1.dat](http://dlib.net/files/dlib_face_recognition_resnet_model_v1.dat.bz2)  
   - Extract and place them in `data/data_dlib/`.

2. **Register your own faces**  
   - Run `python get_faces_from_camera_tkinter.py` to capture face images.
   - Run `python features_extraction_to_csv.py` to generate features.

---

## Setup & Installation

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   cd Attendance
   ```

2. **Install dependencies:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

3. **Download dlib models:**  
   Place `shape_predictor_68_face_landmarks.dat` and `dlib_face_recognition_resnet_model_v1.dat` in `data/data_dlib/`.  
   (These files are large and must be downloaded separately from the official dlib model zoo.)

---

## Usage

### 1. Register Faces

Run the Tkinter GUI to register new users:
```bash
python get_faces_from_camera_tkinter.py
```
- Enter a name, capture face images, and save. Images are stored in `data/data_faces_from_camera/`.

### 2. Extract Features

After registering faces, extract features:
```bash
python features_extraction_to_csv.py
```
- This generates/updates `data/features_all.csv`.

### 3. Start Attendance Recognition

Run the real-time recognition and attendance marking:
```bash
python attendance_taker.py
```
- Recognized faces are marked present in `attendance.db` with timestamp and date.

### 4. View Attendance

Start the Flask web server:
```bash
python app.py
```
- Visit [http://localhost:5000](http://localhost:5000) to select a date and view attendance records.

---

## Technical Details

- **Face Detection & Recognition:**  
  Uses dlib's HOG-based detector and ResNet-based 128D face embeddings. Recognition is performed by comparing embeddings with a Euclidean distance threshold.
- **Database:**  
  Attendance is stored in SQLite (`attendance.db`), with uniqueness enforced per user per day.
- **Web UI:**  
  Flask serves a Bootstrap-styled HTML page for querying attendance by date.

---

## Notes

- **Do NOT commit:**  
  - `venv/`, `attendance.db`, `data/data_dlib/`, `data/data_faces_from_camera/`, `data/features_all.csv`
- **Model files** must be downloaded separately due to size and licensing.

---

## Project Screenshots
<img width="935" height="554" alt="image" src="https://github.com/user-attachments/assets/5e77e80a-e74d-4dd3-908b-5a0dc621e1dc" />

<img width="1083" height="807" alt="image" src="https://github.com/user-attachments/assets/7e1631dc-ea89-4608-b041-abb83764b769" />


## Requirements

- Python 3.8+
- dlib, numpy, scikit-image, pandas, opencv-python, flask

---

