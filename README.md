# VIVISIERA

import cv2
import time
import pandas as pd
from datetime import datetime

# Initialize variables
static_back = None
motion_list = [None, None]
time = []
df = pd.DataFrame(columns=["Start", "End"])

# Capture video from the webcam
video = cv2.VideoCapture(0)

while True:
    check, frame = video.read()
    motion = 0
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    gray = cv2.GaussianBlur(gray, (21, 21), 0)

    if static_back is None:
        static_back = gray
        continue

    diff_frame = cv2.absdiff(static_back, gray)
    thresh_frame = cv2.threshold(diff_frame, 30, 255, cv2.THRESH_BINARY)[1]
    thresh_frame = cv2.dilate(thresh_frame, None, iterations=2)

    contours, _ = cv2.findContours(thresh_frame.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    for contour in contours:
        if cv2.contourArea(contour) < 10000:
            continue
        motion = 1
        (x, y, w, h) = cv2.boundingRect(contour)
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 3)

    motion_list.append(motion)
    motion_list = motion_list[-2:]

    if motion_list[-1] == 1 and motion_list[-2] == 0:
        time.append(datetime.now())
    if motion_list[-1] == 0 and motion_list[-2] == 1:
        time.append(datetime.now())

    cv2.imshow("Gray Frame", gray)
    cv2.imshow("Difference Frame", diff_frame)
    cv2.imshow("Threshold Frame", thresh_frame)
    cv2.imshow("Color Frame", frame)

    key = cv2.waitKey(1)
    if key == ord('q'):
        if motion == 1:
            time.append(datetime.now())
        break

for i in range(0, len(time), 2):
    df = df.append({"Start": time[i], "End": time[i + 1]}, ignore_index=True)

df.to_csv("Time_of_movements.csv")

video.release()
cv2.destroyAllWindows() from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from <sdk-package-name>.example_service_v1 import *

# Create the authenticator.
authenticator = IAMAuthenticator(' "28vucNZOLQY_2ebNqn8RTvQcOX203hjTCYc8uoHcBtrh"')

# Construct the service instance.
service = ExampleServiceV1(authenticator=authenticator)

import cv2
import time
import pandas as pd
from datetime import datetime

# Initialize variables
static_back = None
motion_list = [None, None]
time = []
df = pd.DataFrame(columns=["Start", "End"])

# Capture video from the webcam
video = cv2.VideoCapture(0)

while True:
    check, frame = video.read()
    if not check:
        break

    motion = 0
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    gray = cv2.GaussianBlur(gray, (21, 21), 0)

    if static_back is None:
        static_back = gray
        continue

    diff_frame = cv2.absdiff(static_back, gray)
    thresh_frame = cv2.threshold(diff_frame, 30, 255, cv2.THRESH_BINARY)[1]
    thresh_frame = cv2.dilate(thresh_frame, None, iterations=2)

    contours, _ = cv2.findContours(thresh_frame.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    for contour in contours:
        if cv2.contourArea(contour) < 10000:
            continue
        motion = 1
        (x, y, w, h) = cv2.boundingRect(contour)
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 3)

    motion_list = [motion_list[-1], motion]

    if motion_list[-1] == 1 and motion_list[-2] == 0:
        time.append(datetime.now())
    if motion_list[-1] == 0 and motion_list[-2] == 1:
        time.append(datetime.now())

    cv2.imshow("Gray Frame", gray)
    cv2.imshow("Difference Frame", diff_frame)
    cv2.imshow("Threshold Frame", thresh_frame)
    cv2.imshow("Color Frame", frame)

    key = cv2.waitKey(1)
    if key == ord('q'):
        if motion == 1:
            time.append(datetime.now())
        break

# Release resources
video.release()
cv2.destroyAllWindows()

# Save motion detection times to a CSV file
for i in range(0, len(time), 2):
    df = df.append({"Start": time[i], "End": time[i + 1]}, ignore_index=True)

df.to_csv("Time_of_movements.csv", index=False)
{
	"name": "visiera",
	"description": "camera detection app",
	"createdAt": "2024-08-26T15:11+0000",
	"apikey": "28vucNZOLQY_2ebNqn8RTvQcOX203hjTCYc8uoHcBtrh"from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
from <sdk-package-name>.example_service_v1 import *

# Create the authenticator.
authenticator = IAMAuthenticator(' "28vucNZOLQY_2ebNqn8RTvQcOX203hjTCYc8uoHcBtrh"')

# Construct the service instance.
service = ExampleServiceV1(authenticator=authenticator)

 



VISIERA
VISIERA is an advanced application designed to detect hidden cameras in public places, ensuring enhanced privacy and security. Whether you’re in a hotel, washroom, park, mall, club, or pub, VISIERA uses state-of-the-art computer vision technology to identify potential surveillance devices and alert you to their presence.

🚀 Features
Hidden Camera Detection: Utilizes sophisticated image processing algorithms to detect cameras hidden in various environments.
Real-Time Alerts: Provides immediate notifications if a potential hidden camera is detected.
User Verification: Implements a secure verification process before and after use to ensure that only authorized users operate the app.
Intuitive Interface: Designed for ease of use, making it accessible to users with different levels of technical expertise.
Future-Proof: Built with extensibility in mind, allowing for future integrations such as thermal imaging and facial recognition.
🌟 Planned Enhancements
Thermal Imaging: Upcoming feature to detect cameras in low-light and obscured conditions.
Face Detection: Planned addition to enhance security by identifying potential surveillance threats through facial recognition.
📂 Installation
Clone the Repository:

bash
Copy code
git clone https://github.com/Pratiksha259311/visiera.git
Open the Solution: Open the VISIERA.sln file in Visual Studio 2022.

Restore Dependencies: Use Visual Studio to restore NuGet packages and other dependencies.

Build and Run: Compile the solution and launch the application to begin detecting hidden cameras.

💡 How It Works
VISIERA employs cutting-edge image analysis techniques to scrutinize real-time video feeds for signs of hidden cameras. With its built-in user verification, it ensures that only authorized individuals can use the application, thereby enhancing security.

🤝 Contributing
We welcome contributions to VISIERA! If you have ideas for improvements or wish to contribute, please follow the guidelines in the CONTRIBUTING.md file. Ensure that your contributions adhere to our coding standards and submit pull requests for review.

📝 License
This project is licensed under the MIT License - see the LICENSE file for details.

💬 Contact
For questions or support, please reach out to me-singhurwashi8@gmail.com.
NOTE: ## Note on IBM Granite

IBM Granite was originally intended to be a part of this project for [specific purpose, e.g., advanced analytics or machine learning]. Unfortunately, due to technical difficulties with the IBM Granite interface, it was not integrated into the final version of the project.




