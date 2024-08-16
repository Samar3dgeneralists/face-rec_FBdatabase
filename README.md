# face-rec_FBdatabase


```markdown
# Face Recognition Web App

## Overview

This project is a face recognition web application built using Python, Azure Face API, and Firebase. The app allows users to register their faces along with personal details like name, age, and gender, which are stored in Firebase. It also supports real-time face detection, identifying registered users and displaying their information. The application uses Flask as the backend framework and can be deployed on platforms like Heroku.

## Features

- **User Registration**: Allows users to register their face along with details like name, age, and gender.
- **Real-Time Face Detection**: Detects faces in real-time and displays the corresponding user information if the face is recognized.
- **OTP-based Authentication**: Users authenticate using their mobile number and OTP, handled via Firebase Authentication.
- **Data Storage**: User information and face data are stored in Firebase Realtime Database.
- **Face Recognition**: Uses Azure Face API for face detection and recognition.

## Project Structure

```
face_recognition_web_app/
│
├── app/
│   ├── __init__.py
│   ├── routes.py
│   ├── utils.py
│   ├── templates/
│   │   └── index.html
│   ├── static/
│       └── styles.css
│
├── firebase/
│   └── firebase_config.json  # Your Firebase credentials file
│
├── requirements.txt  # List of Python dependencies
├── Procfile  # For deploying on Heroku
├── app.py  # Entry point for the Flask app
├── README.md  # Documentation
└── .env  # Environment variables (not committed to version control)
```

## Setup Instructions

### 1. Prerequisites

- **Python 3.x**: Ensure Python is installed.
- **Firebase Account**: Sign up for a Firebase account.
- **Azure Account**: Sign up for an Azure account.
- **IDE**: A code editor like VSCode or PyCharm.
- **Heroku Account**: Sign up for a Heroku account if deploying on Heroku.

### 2. Installation

#### 2.1 Clone the Repository

```bash
git clone https://github.com/yourusername/face_recognition_web_app.git
cd face_recognition_web_app
```

#### 2.2 Create a Virtual Environment

```bash
python -m venv face_recognition_env
source face_recognition_env/bin/activate  # On Windows: face_recognition_env\Scripts\activate
```

#### 2.3 Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Firebase Setup

1. Go to the Firebase Console and create a new project.
2. Enable Authentication: Go to Authentication -> Sign-in method -> Enable Phone.
3. Create a Realtime Database: Choose the Realtime Database option and set it to test mode.
4. Download the `firebase_config.json` credentials file and place it in the `firebase/` directory.
5. Add Firebase configuration details to the `.env` file.

### 4. Azure Face API Setup

1. Go to the Azure Portal and create a Face API resource.
2. Get the API Key and Endpoint from the Face API resource overview page.
3. Set up a Person Group in Azure, which will store face data of registered users.
4. Add the Azure API details to the `.env` file.

### 5. Running the Application

#### 5.1 Start the Flask Application

```bash
python app.py
```

The app will be accessible at `http://127.0.0.1:5000/`.

### 6. Deployment

#### 6.1 Deploying to Heroku

1. Create a Heroku app:

```bash
heroku create face-recognition-app
```

2. Push the project to Heroku:

```bash
git push heroku main
```

3. Set up the Firebase and Azure configuration variables in Heroku:

```bash
heroku config:set FIREBASE_DB_URL=your_firebase_db_url
heroku config:set AZURE_SUBSCRIPTION_KEY=your_azure_subscription_key
heroku config:set AZURE_FACE_API_ENDPOINT=your_azure_face_api_endpoint
```

### 7. How It Works

#### 7.1 Registration Process

- The user submits their personal details along with a face image.
- The face image is processed and sent to Azure Face API, which creates a person in a specified person group.
- The user's data, including the `person_id` generated by Azure, is stored in Firebase Realtime Database.

#### 7.2 Real-Time Face Detection

- The app captures a face image and sends it to Azure Face API for detection and identification.
- If a match is found, the corresponding user data is retrieved from Firebase and displayed.
- If no match is found, a message prompts the user to register.

### 8. Firebase Database Structure

The Firebase Realtime Database is structured as follows:

```
/users
  |__ <user_id>
        |__ name: "John Doe"
        |__ age: 30
        |__ gender: "Male"
        |__ mobile_number: "+1234567890"
        |__ person_id: "personId_from_Azure"
```

### 9. Code Explanation

- **`app/routes.py`**: Contains the Flask routes for registration and face detection.
- **`app/utils.py`**: Utility functions for interacting with Azure Face API.
- **`app/templates/index.html`**: Simple HTML file to display user information.
- **`.env`**: Stores sensitive environment variables.

### 10. Troubleshooting

- **Issue**: Azure Face API is not recognizing faces.
  - **Solution**: Ensure the image quality is good and the person group has been trained after adding faces.
  
- **Issue**: Firebase is not storing data.
  - **Solution**: Double-check the Firebase database URL and ensure the Firebase Admin SDK is correctly initialized.

## Contributing

Feel free to fork this repository, submit issues, and make pull requests.

## License

This project is licensed under the MIT License.
```

You can copy this content into a text editor and save it as `README.md`. Let me know if you need any further assistance!
