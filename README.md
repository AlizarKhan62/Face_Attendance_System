# Face Attendance System 👨‍🎓

A comprehensive face recognition-based attendance management system built with Python, OpenCV, and MySQL. This system allows automated student attendance marking through facial recognition technology.

## 📋 Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [System Requirements](#system-requirements)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [Modules Description](#modules-description)
- [How It Works](#how-it-works)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- **User Authentication**: Secure login and registration system
- **Student Management**: Add, update, delete, and view student details
- **Face Data Collection**: Capture multiple images of students for training
- **Face Recognition**: Real-time face detection and recognition using LBPH (Local Binary Pattern Histogram)
- **Automated Attendance**: Automatically mark attendance when a face is recognized
- **Attendance Management**: View, export, and manage attendance records
- **CSV Export**: Export attendance data to CSV format
- **Developer Information**: Information about the development team
- **Help Section**: User guidance and instructions

## 🛠️ Technologies Used

- **Python 3.x** - Core programming language
- **OpenCV (cv2)** - Computer vision and face recognition
- **Tkinter** - GUI framework
- **PIL (Pillow)** - Image processing
- **MySQL** - Database management
- **NumPy** - Numerical operations
- **Haar Cascade** - Face detection classifier
- **LBPH Face Recognizer** - Face recognition algorithm

## 💻 System Requirements

- Python 3.7 or higher
- MySQL Server 5.7 or higher
- Webcam (for capturing images)
- Windows/Linux/MacOS
- Minimum 4GB RAM
- 500MB free disk space

## 📦 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/AlizarKhan62/Face_Attendance_System.git
cd Face_Attendance_System
```

### 2. Install Required Packages
```bash
pip install opencv-python
pip install opencv-contrib-python
pip install pillow
pip install numpy
pip install mysql-connector-python
pip install tkinter
```

### 3. Install MySQL Server
Download and install MySQL Server from [MySQL Official Website](https://dev.mysql.com/downloads/mysql/)

## 🗄️ Database Setup

### 1. Create Database
```sql
CREATE DATABASE face_recog;
USE face_recog;
```

### 2. Create Student Table
```sql
CREATE TABLE student (
    Dep VARCHAR(100),
    Course VARCHAR(100),
    Year VARCHAR(50),
    Semester VARCHAR(50),
    Student_id INT PRIMARY KEY,
    Name VARCHAR(100),
    Division VARCHAR(50),
    Roll VARCHAR(50),
    Gender VARCHAR(20),
    Dob VARCHAR(50),
    Email VARCHAR(100),
    Phone VARCHAR(50),
    Address TEXT,
    Teacher VARCHAR(100),
    PhotoSample VARCHAR(10)
);
```

### 3. Create Register Table
```sql
CREATE TABLE register (
    fname VARCHAR(50),
    lname VARCHAR(50),
    contact VARCHAR(50),
    email VARCHAR(100),
    securityQ VARCHAR(200),
    securityA VARCHAR(200),
    password VARCHAR(50)
);
```

### 4. Update Database Credentials
Update the MySQL connection details in the following files:
- `face_recognition.py`
- `student.py`
- `login.py`
- `register.py`

Replace:
```python
conn = mysql.connector.connect(
    host='localhost',
    username='root',
    password='your_password',  # Change this
    database='face_recog'
)
```

## 📁 Project Structure

```
Face_Attendence_System/
│
├── main.py                  # Main application window
├── login.py                 # User login interface
├── register.py              # User registration interface
├── student.py               # Student management module
├── train.py                 # Face data training module
├── face_recognition.py      # Face recognition and attendance marking
├── attendance.py            # Attendance management module
├── developer.py             # Developer information
├── help.py                  # Help and instructions
│
├── data/                    # Captured face images for training
│   └── user.*.*.jpg
│
├── college_images/          # GUI images and backgrounds
│
├── classifier.xml           # Trained face recognition model
├── haarcascade_frontalface_default.xml  # Face detection model
├── attendance.csv           # Attendance records
└── README.md               # This file
```

## 🚀 Usage

### 1. Start the Application
```bash
python login.py
```

### 2. Register a New User
- Click on "New User Register" button
- Fill in the registration details
- Click "Register" to create an account

### 3. Login
- Enter your username and password
- Click "Login" to access the main dashboard

### 4. Add Student Details
- Click on "Student Details" button
- Fill in student information (Department, Course, Year, etc.)
- Click "Take Photo Sample" to capture face images
- The system will capture 100 images of the student's face
- Click "Save" to store student details in database

### 5. Train the Model
- Click on "Face Detector" button (or navigate to Train Data section)
- Click "TRAIN DATA" button
- Wait for the training process to complete
- A message will confirm when training is done

### 6. Mark Attendance
- Click on "Face Detector" button
- Click "Face Recognition" button
- The webcam will open and start detecting faces
- When a registered face is detected, attendance is automatically marked
- Attendance is saved in `attendance.csv`

### 7. View Attendance
- Click on "Attendance" button
- View all attendance records
- Use "Import CSV" to import existing data
- Use "Export CSV" to save attendance records
- Reset or delete records as needed

## 📚 Modules Description

### main.py
The main dashboard that provides navigation to all modules including Student Details, Face Detection, Attendance, Help, and Developer Info.

### login.py
Handles user authentication with username and password validation against the MySQL database. Includes password reset functionality.

### register.py
Allows new users to create accounts with personal information and security questions for password recovery.

### student.py
Complete student management system with CRUD operations:
- Add new students
- Update student information
- Delete student records
- Capture face samples (100 images per student)
- Search and filter students

### train.py
Trains the LBPH Face Recognizer using captured images from the `data/` directory. Creates/updates the `classifier.xml` file.

### face_recognition.py
Real-time face detection and recognition:
- Uses Haar Cascade for face detection
- LBPH algorithm for face recognition
- Confidence threshold of 77% for accurate recognition
- Automatically marks attendance in CSV file
- Displays student information overlay on detected faces

### attendance.py
Manages attendance records:
- View all attendance entries
- Import/Export CSV files
- Search and filter records
- Update or delete attendance entries

### developer.py
Displays information about the development team and project contributors.

### help.py
Provides user instructions and guidance on how to use the system.

## 🔧 How It Works

### 1. Face Detection
- Uses Haar Cascade Classifier (`haarcascade_frontalface_default.xml`)
- Detects faces in real-time from webcam feed
- Converts images to grayscale for processing

### 2. Face Recognition
- Uses LBPH (Local Binary Pattern Histogram) algorithm
- Trained on 100+ images per student
- Compares detected faces with trained model
- Confidence threshold: 77%
- Returns student ID and confidence score

### 3. Training Process
- Collects 100 images per student from webcam
- Stores images in `data/` folder with naming convention: `user.[ID].[number].jpg`
- Converts images to grayscale
- Trains LBPH recognizer
- Saves trained model as `classifier.xml`

### 4. Attendance Marking
- When face is recognized with >77% confidence
- Fetches student details from database
- Checks if attendance already marked for the day
- Records timestamp and date
- Saves entry to `attendance.csv`

## 📸 Screenshots

*Add your application screenshots here*

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/improvement`)
3. Make your changes
4. Commit your changes (`git commit -am 'Add new feature'`)
5. Push to the branch (`git push origin feature/improvement`)
6. Create a Pull Request

## 📝 Notes

- Ensure good lighting conditions for accurate face recognition
- Keep the camera steady during image capture
- Train the model after adding new students
- The confidence threshold can be adjusted in `face_recognition.py`
- Regular database backups are recommended

## ⚠️ Troubleshooting

### Common Issues:

**1. MySQL Connection Error**
- Verify MySQL server is running
- Check database credentials in Python files
- Ensure `face_recog` database exists

**2. Camera Not Working**
- Check webcam permissions
- Verify camera is not being used by another application
- Try changing camera index in code (cv2.VideoCapture(0) to cv2.VideoCapture(1))

**3. Face Not Detected**
- Ensure adequate lighting
- Face should be clearly visible
- Check if `haarcascade_frontalface_default.xml` exists

**4. Low Recognition Accuracy**
- Capture more training images
- Retrain the model
- Adjust confidence threshold
- Ensure varied face angles during training

## 📧 Contact

For any queries or support, please contact:
- GitHub: [@AlizarKhan62](https://github.com/AlizarKhan62)

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

**Note**: This system is designed for educational purposes. Ensure compliance with privacy regulations and obtain necessary permissions before deploying in production environments.

## 🔮 Future Enhancements

- [ ] Multi-face recognition in single frame
- [ ] Mobile application integration
- [ ] Email/SMS notifications
- [ ] Dashboard with analytics and reports
- [ ] Integration with other biometric systems
- [ ] Cloud database support
- [ ] Improved UI/UX design
- [ ] Multi-language support
- [ ] Automated report generation

---

**Happy Coding! 🚀**
