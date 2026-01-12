# Facial Recognition Attendance System

A Python-based attendance system that uses facial recognition technology to automatically identify and record employee/student attendance using face recognition and a MySQL database.

## Features

- **Facial Recognition**: Uses OpenCV and Haar Cascades for face detection and LBPH (Local Binary Patterns Histograms) for face recognition
- **Automated Attendance Tracking**: Automatically records attendance when a face is recognized
- **Database Integration**: Stores attendance records in a MySQL database with timestamps
- **Multiple Detection Modes**: Detects faces, eyes, and smiles for enhanced accuracy
- **Easy Training**: Simple face training process to add new users to the system
- **Tkinter GUI**: User-friendly graphical interface for interaction

## Project Structure

```
├── attendance.py          # Initializes MySQL database and creates necessary tables
├── face-train.py          # Trains the face recognition model using images
├── face.py                # Main face recognition and attendance recording module
├── labels.pickles         # Serialized label mappings for recognized faces
├── requirements.txt       # Python dependencies
├── cascades/              # Haar Cascade XML files for detection
│   └── data/
│       ├── haarcascade_frontalface_alt2.xml
│       ├── haarcascade_eye.xml
│       ├── haarcascade_smile.xml
│       └── [other cascade files]
├── images/                # Training images organized by person name
│   ├── Brian/
│   ├── Elon_Musk/
│   ├── Obama/
│   └── [other person folders]
└── recognizers/           # Trained face recognition models
    └── face-trainner.yml
```

## Prerequisites

- Python 3.7 or higher
- MySQL Server
- Webcam or camera for attendance tracking

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd Facial_Recognition_Attendance_System
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure MySQL Database**:
   - Ensure MySQL is running on your system
   - Update database credentials in the scripts or use environment variables:
     - Create a `.env` file in the project root with:
       ```
       DB_HOST=localhost
       DB_USER=your_mysql_user
       DB_PASSWORD=your_mysql_password
       ```

## Usage

### Step 1: Initialize the Database

Run this once to create the necessary database and tables:

```bash
python attendance.py
```

This creates:
- A database named `ATTENDANCE`
- A table `UserAttendance` with columns: `Date`, `USERNAME`, and `DateTime`

### Step 2: Prepare Training Images

1. Create a folder for each person in the `images/` directory (use their name or ID)
2. Add photos of that person to their folder (JPG, JPEG, or PNG format)
3. Ensure good lighting and various angles for better accuracy

Example structure:
```
images/
├── John_Doe/
│   ├── photo1.jpg
│   ├── photo2.jpg
│   └── photo3.jpg
├── Jane_Smith/
│   ├── photo1.jpg
│   ├── photo2.jpg
│   └── photo3.jpg
```

### Step 3: Train the Model

Train the face recognition model with your images:

```bash
python face-train.py
```

This generates `labels.pickles` and updates `recognizers/face-trainner.yml`

### Step 4: Run Attendance System

Start the attendance recording system:

```bash
python face.py
```

The system will:
- Open your webcam
- Detect faces in real-time
- Recognize trained faces
- Record attendance with timestamp in the database

## Dependencies

- **opencv-contrib-python**: Computer vision library for face detection and recognition
- **numpy**: Numerical computations
- **Pillow**: Image processing
- **mysql-connector-python**: MySQL database connectivity
- **python-dotenv**: Environment variable management

## Haar Cascade Classifiers

The system uses pre-trained Haar Cascade classifiers for detection:
- `haarcascade_frontalface_alt2.xml` - Front face detection
- `haarcascade_eye.xml` - Eye detection
- `haarcascade_smile.xml` - Smile detection

## File Descriptions

| File | Purpose |
|------|---------|
| `attendance.py` | Database setup and initialization |
| `face-train.py` | Model training using labeled face images |
| `face.py` | Main application for real-time face recognition and attendance |
| `labels.pickles` | Serialized person-to-ID mappings |
| `recognizers/face-trainner.yml` | Trained LBPH face recognizer model |

## Configuration

You can configure database connection details using environment variables in a `.env` file:

```env
DB_HOST=localhost
DB_USER=your_username
DB_PASSWORD=your_password
DB_NAME=attendance
```

Or modify the hardcoded values in the scripts directly.

## Troubleshooting

- **No faces detected**: Ensure good lighting and clear camera feed
- **Database connection errors**: Check MySQL is running and credentials are correct
- **Poor recognition accuracy**: Add more training images with various angles and lighting conditions
- **Missing cascade files**: Verify all XML files are present in `cascades/data/`

## Future Enhancements

- Add web interface for attendance viewing
- Implement attendance reports and analytics
- Add support for multiple camera feeds
- Real-time performance metrics
- Export attendance to CSV/PDF

## License

This project is open source and available under the MIT License.

## Author

Created for automated attendance tracking using facial recognition technology.

## Support

For issues, questions, or suggestions, please create an issue in the repository.
