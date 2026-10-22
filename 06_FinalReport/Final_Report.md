# ZiGym: A Mobile Fitness App with Real-Time Exercise Form Feedback Using On-Device Pose Detection

**Faculty of Computing and Engineering — Bachelor of Computer Science (Hons)**
**BCS3115 Final Year Project 2 — Project Report**

| | |
|---|---|
| **Prepared by** | Siew Zi Hao (QIU202407-007484) |
| **Supervisor** | Mr Muhamad Amirul Asyraf Rahmat |
| **Moderator** | Ms Yew Yean Yoong |

## Acknowledgments

I would like to express my deepest gratitude to my project supervisor, Mr. Muhamad Amirul Asyraf Rahmat, for his invaluable guidance, constructive comments, and insightful suggestions throughout the development of this project.

I am also sincerely thankful to my friends, whose constant support, input, and encouragement have been a source of strength during this journey.

Finally, I owe my heartfelt appreciation to my family for their inexhaustible love, patience, and understanding.

> **TODO:** the acknowledgments above are shortened; paste your full wording from the Word report. Check the course code (the cover of the Word report says BCS3118) and the submission date.

---

## Abstract

Many people exercise without a coach and cannot tell whether their form is correct, which can reduce the benefit of a workout and increase the risk of injury. This project presents ZiGym, an Android application built with Flutter that counts repetitions and gives live form feedback through the phone camera. It uses Google ML Kit Pose Detection to locate body landmarks on the device, and Firebase for accounts and stored records.

Instead of a trained model or an external AI service, ZiGym applies rule-based algorithms to the landmark coordinates. For Push-Up, Squat, Jumping Jack and Plank it checks joint angles, body alignment, left and right symmetry, rep tempo and camera distance, and it reports one issue per rep as text, red highlighting on a skeleton overlay and spoken feedback. The app also provides a form summary, progress dashboard, history-based recommendations, workout recordings and offline handling. All analysis runs on the phone, so there is no running cost and camera images are not sent anywhere.

The system was tested during development, by a person who had not used the app, with recordings made on a physical phone, and with a user survey. **[TODO: Fill in: the number of survey respondents and the main result.]** Testing fixed problems such as still objects being detected as a person. It also showed that the form checks depend on camera placement: good-form reps filmed from the front were flagged as faulty, and side-view recordings showed that the person-presence check was too strict until it was revised. The thresholds are estimates that have not been validated on labelled data.

The project shows that useful real-time form feedback can run on an ordinary phone when the camera is positioned correctly. A trained model, per-exercise thresholds and calibration to body proportions are the main future directions.

*Keywords: pose estimation, exercise form analysis, mobile application, Flutter, Google ML Kit*

---

## List of Abbreviations

|        |                                                              |
|--------|--------------------------------------------------------------|
| 2D     | Two-dimensional                                              |
| AI     | Artificial Intelligence                                      |
| API    | Application Programming Interface                            |
| APK    | Android Package Kit                                          |
| BMI    | Body Mass Index                                              |
| CSV    | Comma-Separated Values                                       |
| FYP    | Final Year Project                                           |
| ML     | Machine Learning                                             |
| ML Kit | Google's on-device machine learning software development kit |
| QIU    | Quest International University                               |
| SWOT   | Strengths, Weaknesses, Opportunities and Threats             |
| TFLite | TensorFlow Lite                                              |
| TTS    | Text-to-Speech                                               |
| UI     | User Interface                                               |

**[TODO: Confirm: add any other abbreviations used in your chapters, such as UML if you use it in Chapter 3, and keep the list in alphabetical order.]**

---

## Contents

1. [Chapter 1: Introduction](#chapter-1-introduction)
2. [Chapter 2: Literature Review](#chapter-2-literature-review)
3. [Chapter 3: Methodology](#chapter-3-methodology)
4. [Chapter 4: Testing](#chapter-4-testing)
5. [Chapter 5: Conclusion](#chapter-5-conclusion)
6. [References](#references)
7. [Appendices](#appendices)

---

# Chapter 1: Introduction

## Chapter Overview

Today's technologically advanced world is increasingly utilizing artificial intelligence (AI) in the health and fitness sector. More people are aware of the importance of exercise, but many do not have a coach or a trainer, and may not be sure that they are doing the exercises correctly. The majority of fitness software log hand-entered workouts, and offer little information on how an exercise is being performed.

The project aims to create a new mobile fitness app to count reps and provide live feedback based on the phone camera and in-device pose detection to confirm exercise form. This chapter includes the project background, the problem statement, the project goals, the project scope and the project benefits as well as project milestones and constraints.

## 1.1 Project Background

With the demands of modern life, it is difficult for many people to maintain a healthy lifestyle because of a lack of time, knowledge and access to professional coaches. Bad posture during a workout can decrease effectiveness and increase risk of injury when working out, including squats and push-ups (Gadhvi et al., 2025).

Artificial Intelligence and Computer Vision now have opened new avenues for fitness applications. Pose estimation models can use a camera to detect the key joints of the human body in real time without the need for additional sensors (Bazarevsky et al., 2020). One such tool is Google ML Kit Pose Detection. It is a mobile app and returns 33 body landmarks per camera frame (Google, n.d.). These landmarks can be used to calculate joint angles and body positions; this can be used to judge how an exercise is being performed.

This project applies this approach to create an Android app called ZiGym. It tallies the number of repetitions for Push Up, Squat and Jumping Jack, times taken for Plank holds, and provides feedback on form in the form of text, highlighted joints on a skeleton overlay, and spoken feedback. The analysis is performed by rule-based algorithms, on the phone, so there is no need of any server for analysis, and no paid AI service.

## 1.2 Problem Statement

While there are many fitness apps out there, there are a few issues that need to be addressed. Secondly, individuals generally do not work with a coach and therefore may not become aware of sub-optimal form (for example, having a sagging back while doing a push up or leaning forward too far when squatting). This can reduce the effectiveness of the exercise and/or cause injury.

Second, the majority of mobile fitness apps offer exercise programs, tutorials and manual logging, but do not communicate with the user during exercise to let them know if their exercise is performed correctly. However, posture feedback systems that rely on cameras frequently require specialized hardware, like smart mirrors, or extra computing power, which can drive up costs and limit access (Sharma & Bohra, 2025; Oh et al., 2023).

Thirdly, the accuracy of camera-based posture analysis is affected by conditions such as lighting, camera position and body occlusion. Users must be instructed how to move the camera, and a system must ascertain whether it can rely on the information it receives before analysing the form.

Thus, an application is required which uses a standard smartphone camera, is not software dependent and requires no running cost on the device; requires the user to track their repetitions; immediately provides feedback on the exercise form (no running cost); and records the progress so that the user can monitor their improvement.

## 1.3 Objectives

This project intends to create an app that will allow people to work out with proper form using just a smartphone camera. Specific objectives are:

To create an Android app that will use in-device pose detection to count repetitions of Push-Up, Squat and Jumping Jack exercises, and to time Plank holds.

2. To develop, design, and implement algorithms that will assess the exercise form based on joint angles, body alignment, left- and right-handedness symmetry, rep tempo, and camera distance, and provide the outcome in real-time as text, visual highlighting, and verbal feedback.

To be able to give a summary of a form after exercise, and also to track the progress and also show inferences based on past exercise in a user profile in the phone, sensibly handling the phone not being connected.

4. To assess the system using manual testing, user testing, and user surveys, and to report the accuracy and limitations of the system truthfully.

## 1.4 Scope

### 1.4.1 In Scope

User accounts: Sign up, log in and an editable profile of name, date of birth, height, weight, fitness goal and profile picture.

Real-time pose detection and repetition counting for Push-Up, Squat and Jumping Jack, as well as hold timing for Plank. Only verifies that the user is in frame (stretching).

Feedback in text, red joint highlighting and spoken feedback is provided with form analysis based on joint angle, body alignment, left and right symmetry, rep tempo and camera distance.

Guidance on positioning the camera on the exercise instruction pages.

Recording, playback and a per-user limit of 5 workouts with the skeleton overlay.

- A summary of the form after training, progress dashboard with achievements, recommendations based on the user's history.

- An approximation of calories burned, based on a set number of calories burned per repetition or per minute of hold.

Offline use: User is clearly informed what is and is not available.

- Android devices only.

### 1.4.2 Out of Scope

No wearable sensors or exercise equipment is involved in the project, and it is a software application.

Not a medical or clinical physiotherapy tool; application provides posture feedback.

These were originally proposed but dropped for the purposes of the project to focus on posture analysis and food recognition and calorie intake tracking. \[Confirm: the reason you give for this change.\]

Built a trained machine-learning model for form classification: a data-collection mode was designed for this purpose, but training and deploying a model is deferred to future work.

Social networking tools, a video personal trainer or online store.

Support for more than one person at a time, and iOS support.

## 1.5 Benefits and significance

The following are advantages of this project. Primarily, it enhances the safety and effectiveness of exercise: the user can see what they're doing and get feedback, which they would not otherwise receive from a coach. Secondly, it requires only a standard smartphone camera, and it does not require a server since the analysis is performed on the camera. Camera images are not sent anywhere, and there is no server cost. Thirdly, live feedback, form summary, progress dashboard, and recommendations all provide a picture of what to do to improve and help motivate the user. The project is also practical and academic in importance. It demonstrates the extent to which simple, explainable rules that can be added to a preexisting pose model can be useful in providing form feedback and shows where they are effective and where they don't work, which is helpful for the future development of this type of application

## 1.6 Milestones and deliverables

 

| phases | activities | outcome/result |
|---|---|---|
| Phase1: Project research | Topics were analyzed, and a proposal was prepared. | Finalized title, scope and problem statement. |
| Phase2: Literature Review | Studied the work related to AI fitness systems and pose estimation. | A brief survey of previous studies and the need to fill the gaps. |
| Phase 3: Requirements Analysis | Identified user needs and the functional and non-functional requirements. | Requirements documentation |
| Phase 4: Systems Design | Designed system architecture, system workflow, and the user interface. | Architecture diagram and interface designs. |
| Phase 5: Prototype Development | Developed the Flutter application using ML Kit pose detection and Firebase accounts, storage, and recording. | Working prototype |
| Phase 6: Algorithm development | Created rep counting, form analysis, feedback, and recommendations. | Analyzing and recommending solutions for the class.. |
| Phase 7: testing and evaluation | Manual testing, testing with a new user, recordings on a physical phone, and a user survey. | Found and fixed defects and test results. |
| Phase 8: Documentation and Presentation | Prepare the final report, user guide, poster, and demonstration. | Final report, User Guide, poster and presentation. |

  

  **Figure 1.6 milestone and deliverables for each phase**

## 1.7 Constraints and limitations

There are a number of constraints in the project. The form analysis is based on one 2D camera view, which means that its reliability is dependent on the camera's position; it is vulnerable to lighting effects and loose-fitting clothing, and other body areas that are hidden. The thresholds are not validated against a labelled dataset; they were selected from general exercise guidance. The system can handle limited exercises; it analyzes one person at a time, and it provides calorie figures – it's only an approximation.

The project was also constrained by limited time to complete the project, and by a lack of specialist equipment or access to a large number of participants. These are the reasons why it's not advisable to use the application as a replacement for a medical practitioner or a professional trainer.

---

# Chapter 2: Literature Review

This chapter summarizes the existing work which is relevant to the project. It includes artificial intelligence in fitness, gym applications, image recognition and pose estimation, exercise posture detection, a comparison of similar systems, and a selection of the technologies used for this project. It culminates in the gap that ZiGym fills.

![Figure 2.0: Literature review mind map](figures/image4.png)

. 

## 2.1 Artificial intelligence

Artificial intelligence (AI), which refers to the ability of computers to simulate human intelligence, such as pattern recognition, decision making and data analysis. In the last few years, the healthcare and fitness industry has seen a significant increase in the adoption of AI, thanks to recent developments in machine learning, computer vision, and real-time data processing (Dwivedi et al., 2023; Topol, 2019). Fitness applications are seeing AI systems taking on more responsibilities to monitor workouts automatically and analyze posture, providing recommendations for improvement, making fitness more accessible and efficient. AI application in fitness systems include human pose estimation. Human pose estimation is one of the primary applications of AI in fitness systems. Pose estimation is the process of determining and tracking positions of body joints by analyzing the camera input and using computer vision. In a recent work, Bazarevsky et al. (2020) demonstrated that a model like BlazePose could accurately extract 33 body keypoints in real time using low computational demands, to be suitable for mobile and low-resource settings. This enables a system to determine the body posture without requiring the use of wearables. Exercise monitoring using posture correction with the help of AI has also been studied (Chen & Yang, 2020; Yadav et al., 2022). Pose Trainer (Chen & Yang, 2020) is a system that utilizes 'pose estimation' to identify posture mistakes in exercise sessions and provide feedback to correct posture, and the results indicate that posture analysis can enhance the accuracy of exercises and minimize the chance of injury. Abhinand et al. (2023) introduced AI fitness trainers for human pose estimation to monitor workout actions and quantify repetitions, noting the potential for AI to boost workout engagement. In this project, Google ML Kit Pose Detection is leveraged to get body landmarks on a phone. The posture analysis is not a trained model: it uses rule-based calculations based on the positions of the landmarks, as outlined in Chapter 3. A trained machine-learning model will be used as future work.

## 2.2 Gym Application

As more and more people are seeking to look into digital ways to keep fit and fit healthy, gym applications have grown popular. Their primary use is to schedule workouts, give exercise instructions and track calories. There are some applications like Nike Training Club and MyFitnessPal that allow users to record their food intake and adhere to the exercise plans, but they are still highly manual, and don't learn from the user's actions. As technology has evolved, gym applications are now more interactive thanks to the development of AI and computer vision. Dedhia et al. (2023) developed a virtual gym assistant with MediaPipe and machine learning to analyze exercise posture and count the repetitions while users work out, and found that their system can enhance exercise performance and reduce the need for personal trainers. Sathish et al. (2025) proposed a fitness application, called Neural Fit, using neural networks to compare poses in order to assess the exercise posture and provide real-time corrective feedback. Personalised and adaptive features are also increasingly becoming a feature. Sharma and Bohra (2025) developed an AI-based smart mirror that gives real-time posture correction and workout monitoring, and found that individual feedback improves the effectiveness of workouts and the motivation of users. Heo et al. (2026) developed an AI-based Adaptive Exercise Prescription System by designing a programme based on the user's fitness level and the performance of his/her actions. These studies demonstrate that present fitness applications have become “smart” assistants, in which fitness, posture and movement are monitored in real-time, and exercises are suggested and recommended. However, many of them still require costly hardware, high implementation costs or additional computing resources and many focus on posture detection and analysis of movement but are not easily deployable for the general public (Kim & Lee, 2025; Oh et al., 2023). Lighting conditions, camera angle and the capabilities of the device also influence the accuracy of posture detection.

## 2.3 Image Recognition

Image recognition is an area of computer vision and artificial intelligence that can identify and interpret objects, people or movements within images and video. In recent years, image recognition has become a valuable tool for many industries, such as healthcare, security, education and fitness, due to the introduction of algorithms in the areas of deep learning and computer vision. In fitness, image recognition can be used to monitor a user's movements and analyse how fitness exercises are being performed in real-time, without requiring any special equipment or sensors. A normal webcam and/or the camera on a smartphone is sufficient to provide virtual training and posture correction. Pose estimation technologies can precisely estimate the position of the body's landmarks and track movement efficiently even on low-resource devices (Bazarevsky et al., 2020; Hsieh & Sun, 2025). ZiGym uses Google ML Kit Pose Detection to detect exercise posture. It detects the shoulder, elbow, hip, knee, ankle points from the camera image in real-time and each point has a confidence value (Google, n.d.). ZiGym uses these landmarks to determine proper execution of the exercise. This enables measurements of the angles of the joints and the alignment of the body when performing movements like squats, push ups and jumping jacks. Accordingly, image recognition can be used to enable real-time error correction. Errors in the movement, such as poor squat depth, back alignment etc. can be detected by a system learning the landmarks identified and how the movement changes over time so that the user can correct the movement and minimise the risk of injury. AI posture correction can make a significant impact on exercise performance and user engagement, reported Chen and Yang (2020). It is also simple and inexpensive to use image recognition. The traditional posture monitoring usually requires wearing the sensors or hiring a professional trainer, which is expensive, less convenient and practicable, and an image recognition system only requires a camera and software. Although these are benefits, it can be affected by the lighting, position of the camera as well as parts of the body being concealed. Recognizing can also be inconsistent as the users are different in size and movement. The design of ZiGym is directly impacted by these issues: Before it is able to judge an exercise, ZiGym must ensure that a person is clearly visible and at an appropriate distance.

## 2.4 Exercise posture detection

A crucial aspect of smart fitness system is posture detection, as being in the wrong posture can lead to injury and decrease the effectiveness of the exercise. The traditional approach to posture monitoring requires a professional trainer or wearable monitoring devices, thus increasing the costs and limiting access. Recent studies indicate that computer vision-based posture detection is more efficient and more cost-effective. MediaPipe Pose is a widely adopted framework for real-time analysis of exercise posture, due to its lightweight design and real-time processing (Bazarevsky et al., 2020; Google, 2024). Google (2024) states that it is possible to identify body landmarks with a normal camera and the location of these can be used to calculate the angle of joints and movements while exercising. Similar to Google ML Kit Pose Detection, this project provides a set of body landmarks on mobile devices (Google, n.d.). Pose estimation has been successfully applied to exercise monitoring by several researchers. Collhins et al. (2026) have created a mobile application using AI, which evaluates exercise posture by pose estimation, and by studying the results, it was concluded that real-time posture feedback can increase the safety of exercise and increase the accuracy of the motion. Haldar (2026) introduced a framework for an intelligent yoga posture correction system that utilizes AI to detect posture and provide corrections. Gadhvi et al. (2025) introduced an edge-AI posture correction system for physical exercises, which was shown to enhance the workout experience and help prevent posture-related injuries. On top of this, Hsieh and Sun (2025) created a posture monitoring app with a low-cost device and demonstrated that pose estimation can be performed on budget devices. Nevertheless, there are challenges in posture detection systems such as light changes, occlusion of the body by other objects, and the distance between the subject and the camera. These factors may decrease the accuracy and reliability of real-time pose estimation in exercise. Despite this, recent studies have demonstrated that pose estimation is still highly effective for developing low-cost accessible fitness monitoring systems that provide real-time posture analysis and feedback via low-cost cameras (Oh et al., 2023; Kim & Lee, 2025).

## 2.5 Comparative Study of Similar Systems (SWOT Analysis)

| System | strength | weakness | opportunities | threats |
|---|---|---|---|---|
| My Fitness Pals | Large food database and calorie tracking | Manual food input required | Integration with ai technologies is planned | Competitive in fitness apps market |
| Nike Training Club | Pro workout plans | Posture analysis is not in real time | Broaden adaptable workout frameworks | User retention issues |
| Virtual gym assistant (Dedhia et al., 2023) | Real-time posture monitoring | Limited exercise variety | Expanded ai exercise recognition | Environmental sensitivity |
| Posture sense smart mirror (Sharma & Bohra, 2025) | Interactive posture feedback | Expensive hardware requirements | Home fitness market growth | Privacy concerns |
| ZiGym Apps | Integrated posture detection and calorie burn estimation with standard camera devices. | Limited exercise support in initial stages | Expand personalization s and ai recommendatio n | Model accuracy limitations |

*Table 2.5: SWOT analysis of similar systems*

  

 ZiGym is a lightweight application which provides feedback on a form in real time without requiring a special camera. Unlike MyFitnessPal which requires manual input, ZiGym automatically tracks movement and evaluates form using ML Kit's pose detection. Nike Training Club has a lot of basic workout routines, but ZiGym reacts to the user's movements in real time. It doesn't require complicated hardware like other smart mirror systems, and it operates on a regular phone, making it more affordable and accessible. However, ZiGym isn't without its limitations. It contains limited exercises, its thresholds have not been compared with the labeled data, and the accuracy is related to the placement of the camera.

## 2.6 Technologies Used

Three main technologies were chosen for the project. Google ML Kit Pose Detection offers the landmarks of the body and confidence level for each landmark. It is installed on the device, making it ideal for an offline, low-cost application (Google, n.d.). The Android application is built using Flutter (Flutter, n.d.) and has a single code base, and the camera and the pose detection plugin is accessed using flutter. Firebase offers user authentication, cloud storage for workout records and user profiles, and storage for pictures of users (Firebase, n.d.). The text-to-speech engine of the phone is used for spoken feedback. The aforementioned tools – YOLOv8, OpenCV and TensorFlow – were not required in the proposal. TensorFlow Lite is still a possibility for further development if a trained form classification model is created.

## 2.7 Research Gap 

The literature reveals that pose estimation can provide real-time exercise feedback, but often the systems reviewed require the use of dedicated hardware, require additional computing resources or a complicated setup, and have been sensitive to the position of the camera and environment. A light (smartphone only) app that works entirely in the device, that makes sense of every comment attribute by a specific measurement, and that is open about its limits. ZiGym has been designed to address this need.

---

# Chapter 3: Methodology

## 3.1 Methodology

The project was developed using an iterative prototype development methodology. This is an appropriate method for this project as the form analysis will rely on a camera, and in addition, the person must be moving. The application versions were tested on the phone, and the findings were used to enhance the next version.

![Figure](figures/image5.png)

Figure 3.1 Methodology software development lifecycle

Prototype methodology phases: 

 

 

| Phases                 | description                                                                                                           |
|------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Project planning       | Set the goals, scope, time frame, tools and feasibility..                                                             |
| Requirement analysis   | Identify the functions and the qualities the application will require.                                                |
| System design          | Designed the architecture, database, screens and algorithm.                                                           |
| Prototype development  | Developed the Flutter application, the ML Kit pose detection, the form analysis, and the Firebase features in phases. |
| System integration     | Assembled the camera, analysis, feedback, recording, and storage modules.                                             |
| Testing and evaluation | Manual testing, testing with a new user, recordings on a physical phone, and a user survey.                           |
| Final implementation   | Fixed the issues, finalized the application, and wrote the documentation.                                             |

The first prototype used the MediaPipe Pose framework (Google, 2024). The pose detection was replaced in the development version to Google ML Kit Pose Detection (Google, n.d.) which provides the same type of 33 body landmarks and integrates seamlessly into the Flutter application. Testing resulted in a few changes to the form analysis, including the camera-distance check and person-presence check. 

 

## 3.2 Project Planning 

The project was designed over the two semesters of FYP1 & FYP2. The proposal, literature review, requirements and design were done in FYP1. FYP2 covered the development, testing and documentation.

![Figure](figures/image2.png)

  *Figure 3.2: Gantt chart for FYP1 and FYP2*

## 3.3 Hardware requirements

| Hardware components | specifications |
|---|---|
| Operating system | Intel Core i5 or AMD Ryzen 5 |
| Ram | Minimum 8gb |
| Handheld camera | Webcam or smartphone camera |
| smartphone | Android smartphone for mobile testing or camera input Android 16.0, HONOR 400 PRO |
| GPU | Nvidia GPU for faster AI processing |
| display | Monitor or laptop screen |
| storage | Minimum 256 SSD |

  Table 3.3 Hardware requirements

The pose detection model runs on the phone without any need to have a GPU or server. By default, the front camera is used, which means that the user can see the screen during exercise.

## 3.4 Software requirements

### 3.4.1 Functional requirements

| **Functional requirements ** | **description **                                                                                                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| User account                 | User can create user, sign in, reset his/her password, log out and edit profile (name, date of birth, height, weight, fitness goal, picture of profile).      |
| Exercise selection           | Push-up, Squat, jumping jack, plank, and Stretching: the user can select the one he or she wants to do and read the instructions, including camera placement. |
| Exercise posture detection   | The system detects the body landmarks from the camera in real time.                                                                                           |
| Repeat count                 | Push-ups, squats, and jumping jacks have repetition counting, while Plank hold is timed.                                                                      |
| Camera Guidance              | The system informs the user of the absence of a person or of being too near or too distant.                                                                   |
| Form feedback                | The system identifies form problems and displays them as text, red joint, and verbal messages.                                                                |
| System tracking              | tracks workout history, weekly chart and achievements.                                                                                                        |

### 3.4.2 Non-Functional Requirements

| Nonfunctional requirement  | description                                                                                                                   |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Real-time performance      | Pose detection and feedback should be in sync with camera, otherwise the user should be getting feedback during the exercise. |
| Usability                  | The user interface should be easy to use and understand, even by someone who has never used it before                         |
| reliability                | The system should not provide feedback when it cannot see the person clearly                                                  |
| Performance efficiency     | The analysis should be efficient and run smoothly on an average Android cellphone.                                            |
| Offline capability         | Workouts can be performed without an internet connection; data will be saved when the connection is restored.                 |
| scalability                | New exercises should be able to be added with minimal change                                                                  |

 

## 3.5 System Architecture

![Figure](figures/image6.png)

Figure 3.5 System architecture diagram

ZiGym has a client application and cloud services. All of the interface, the camera, the pose detection and the form analysis are performed by the Flutter application on the phone. The backend is provided by Firebase (Firebase, n.d.): Firebase Authentication is used for user accounts, Cloud Firestore is used to store user profiles and workout data, and Firebase Storage is used to store user profile pictures. The camera frames are passed to the Google ML Kit Pose Detection on the phone. The landmarks it returns are analysed by the rule-based form analysis, which will result in the rep count and the feedback displayed to the user. Data only saved to Cloud Firestore includes the results of the workout, including exercise, reps, duration and any issues detected. These images are not sent out for analysis.

## 3.6 System Framework

| **components **       | **technology **          |
|-----------------------|--------------------------|
| frontend              | flutter                  |
| Programming language  | dart                     |
| Backend services      | firebase                 |
| authentication        | Firebase authentication  |
| database              | Cloud Firestore          |
| Ai model              | Google ml pose kit       |
| Development ide       | Android studio           |

> **Table 3.5 System framework**

## 3.7 UI Design

### 3.7.1 splash screen

![Figure](figures/image7.jpeg)

**Figure 3.6.1 splash screen**

The Splash Screen is the first screen that appears when users start the application of Zi Gym. It is mainly used to introduce the application branding and have a smooth transition before loading the system resources that are needed. In this phase, we initialize Firebase services and determine if the user is authenticated. 

 

After loading, the system automatically checks to see if the user has already logged in or not. If the user is logged in, they will be redirected to the Home Page, otherwise (if they are new or not logged in), they will be redirected to the Login Page. This not only improves user experience but also helps to maintain user engagement by reducing the number of login steps required.

### 3.7.2 Sign up page 

![Figure](figures/image8.jpeg)

** Figure 3.6.2 signup page**

The Signup Page allows new users to sign up for the Zi Gym app. In registering, the users must enter their personal information such as name, age, weight, height, email, and password. This information is gathered to tailor fit the fitness experience and help with BMI calculations. 

 

Once an account is registered successfully, Firebase Authentication generates the user account and Cloud Fire store saves the Firebase user's profile details to the database. After user registration, they can log in and use the app's fitness tracking features.**  **

### 3.7.3 Login page 

![Figure](figures/image9.jpeg)

**Figure 3.6.3 Login page for Zigym app**

The Login Page enables safe and secure login to the Zi Gym application for registered users. Users must provide their email address and password, which will be checked against Firebase Authentication. There are validation mechanisms that will make sure that before trying to log in, the username and password are entered correctly. 

 

If authentication is successful, users get redirected to the Home Page. An error message is shown if invalid credentials are provided, alerting users of the problem. For new users, the page includes a link to the Signup Page, and for users who forgot their password, there is a link to the Reset Password Page.**  **

### 3.7.4 Reset password page 

![Figure](figures/image10.jpeg)

**Figure 3.6.4 reset password page**

The Reset Password Page helps users if they have forgotten their account passwords. Users enter his/her registered email id and requests for reset password using Firebase Authentication. This allows for better accessibility of the accounts and minimizes the need for user intervention by the admin. 

 

If the submission is successful, Firebase will send the user a password reset email to the email address they registered with. Once users have done that, they can get a new password using the instructions they see in the email message, without the risk of someone else obtaining it.**  **

### 3.7.5 Home page(dashboard) 

![Figure](figures/image11.jpeg)

![Figure](figures/image12.jpeg)

**Figure 3.6.5 home page**

The Home page is the primary page after logging in. It provides access to exercise categories, the progress dashboard, the recommendations, and the profile.

### 3.7.6 Strength Training Exercise Page 

![Figure](figures/image13.jpeg)

Figure 3.6.6 exercise categories- strength training page

In the Strength Training section, users can choose from a list of exercises to build muscle, including Push-up and Squat. The exercises presented on each exercise card include the name of the exercise, the level of difficulty, how many calories are burned and a brief description of the muscles targeted. This information enables the users to select exercises that are suited to their fitness goals and their current fitness level. 

 

If the user clicks on Start Workout, the application will go to the AI workout monitoring page. The Google ML PoseKit system then kicks in to assess body posture, count repetitions, and offer feedback on the exercise session as it happens. When the workout is completed, workout information (reps, time, etc.) is saved in Cloud Firestore for progress tracking.**  **

![Figure](figures/image14.jpeg)

### 3.7.7 Cardio, Core Training, and Flexibility Exercise Page 

 

The Cardio, Core Training, and Flexibility sections offer further exercise choices to supplement fitness and wellness. Cardio activities like Jumping Jacks aim to enhance cardiovascular stamina and calories burned. Core exercises strengthen muscles in the abdomen and stabilizers e.g., plank)Flexibility exercises – mobility, flexibility, and recovery, e.g., stretching. 

 

Each exercise card includes appropriate details such as exercise difficulty, an estimated calorie burn rate, and an exercise purpose, just like the Strength Training section. After the selection of a workout, the system starts the AI posture detection module, with this module observing how the workout is performed and giving comments. All workout outcomes are stored in Firebase Firestore, so users can see how they're doing and have a full workout record.** **

### 3.7.8 Progress tracking page

![Figure](figures/image3.jpeg)

The Progress Tracking Page saves and tracks users' exercise activity. The system records details like exercise type, workout length, reps worked, and calories burned while working out. 

These records are kept in Cloud Firestore for future use. 

 

When you exercise using the device, all the data gathered allows you to track your fitness throughout the process. The system keeps a record of completed exercises, which fosters consistency and allows users to track their progress towards fitness targets.**  **

### 3.7.9 Profile Page

![Figure](figures/image15.jpeg)

The Profile Page allows users to view their personal and fitness-related information. The user information, such as name, email, age, weight and height, is fetched from Cloud Firestore and shown in a neat manner. All of this information gives the user a general idea of his/her account and physical measurements. 

 

The page also auto-calculates the user's Body Mass Index (BMI) based on stored height and weight parameters. The Profile Page is also crucial for tracking fitness development over time, as users can access their fitness statistics, achievements, and progress summaries.**  **

### 3.7.10 Logout Page

![Figure](figures/image16.jpeg)

The Logout function will help the user to properly end his current session. A confirmation dialog is displayed when the Logout button is clicked, to avoid accidental logouts. This will prevent users from accidentally losing their accounts. 

 

If the user is successfully authenticated, Firebase Authentication ends the current session and sends the user back to the Login Page. This feature ensures the security of accounts, especially on shared devices.

## 3.8 Use Case Diagram

![Figure](figures/image17.png)

The user is the protagonist. The Sign Up, Log In, Reset Password, Edit Profile, Select Exercise, Read Instructions, Perform Workout, Record Workout, View Recordings, View Workout Summary, View Progress, View Recommendations, and Log Out use cases are used. The account use cases are handled by Firebase Authentication, saving and viewing of data is handled by Cloud Firestore and Firebase Storage, and handling of the Perform Workout use case is done through Google ML Kit. Include a use case diagram (Fig. 3.14). Switch from MediaPipe AI to Google ML Kit, and add the new use cases.

### 3.8.1 Activity Diagram

![Figure](figures/image18.png)

User accesses the application and logs in to begin the activity. The user then selects an exercise and reads the instructions, and starts the workout. The system validates that a person is clearly visible and at an appropriate distance from the camera, for each camera frame, it verifies the validity of the joint angles, it counts the repetitions and provides feedback. At the end of the exercise**,** a summary is displayed and the result is stored. A detailed description of the flow per frame is provided in Section 3.9. Include a figure containing an Activity diagram (Figure 3.15). Display the person and framing checks as decisions prior to the analysis.

### 3.8.2 Class Diagram

![Figure](figures/image19.jpeg)

** **There are three main classes: User, Workout Session and Recording. Each User may have many Workout Sessions. A Workout Session will show the exercise, as well as the number of reps or hold time, duration, estimated calories, date, and the number of form problems identified. The classes and fields in the Exercise and Posture classes from FYP1 should be deleted or renamed, as they will be replaced by the rule-based analysis in Section 3.9.

## 3.9 Form Analysis Algorithm Design

### 3.9.1 Chapter Overview

This section explains how ZiGym turns the output of a pose detection model into repetition counts and form feedback. It describes the complete processing pipeline, the checks that decide whether a camera frame can be trusted, the rules used for each exercise, the order in which problems are reported, and how the per-rep results feed the form summary and the recommendations. The thresholds quoted here are the values used in the app. They are reasoned estimates and have not been validated against a labelled dataset, as discussed in Section 5.1.

### 3.9.2 Design Approach

The form analysis is rule-based and runs entirely on the phone. I chose this over an external AI service or a trained model for four reasons. First, it costs nothing to run. Second, it works without an internet connection. Third, camera images do not leave the device. Fourth, every message the app shows can be traced to a specific measurement, such as an elbow angle or the time a rep took, which makes the behaviour explainable and easier to test. The trade-off is that the system only recognises the problems I wrote rules for.

The input is the output of Google ML Kit Pose Detection, which returns 33 body landmarks for each camera frame. Each landmark has an image position (x and y) and a likelihood value between 0 and 1 that says how confident the model is that the point is correctly located. ZiGym uses only these numbers. It does not use the pixel data itself.

### 3.9.3 Processing Pipeline

Every camera frame passes through the same sequence of steps, shown in Figure 3.17. The first two steps decide whether the frame can be trusted at all, so that the exercise-specific rules never run on a frame with no real person or a badly framed person.

![Figure](figures/8016f1797f08e1006604d5c58518ffee59b25775.png)

Figure 3.17: Form analysis pipeline

### 3.9.4 Measuring Joint Angles

The angle at a joint is calculated from three landmarks. For a joint B with neighbouring landmarks A and C, the angle is the difference between the directions of the lines B to A and B to C, found with the arctangent function and converted to degrees:

> angle = \| atan2(Cy - By, Cx - Bx) - atan2(Ay - By, Ax - Bx) \| x (180 / pi)
>
> if angle \> 180 then angle = 360 - angle

This gives a value from 0 to 180 degrees. For example, the elbow angle uses the shoulder, elbow and wrist, and the knee angle uses the hip, knee and ankle. Body alignment uses the shoulder, hip and ankle, and torso lean uses the shoulder, hip and knee.

### 3.9.5 Choosing the Visible Side

Most angle checks only need one side of the body. For each such check, the app compares the left-side and right-side landmark triplets and uses the side whose landmarks have the higher average confidence. This means the user can face either direction when filmed from the side. A landmark is only used if its likelihood is at least 0.6.

### 3.9.6 Person-Presence Check

ML Kit sometimes reports a few moderately confident landmarks on objects such as a pillow or a stuffed toy. To avoid counting reps with nobody in front of the camera, a frame is accepted only if a chain of nose, shoulder, hip and knee landmarks on at least one side of the body satisfies all of these conditions:

- each of the four landmarks has a likelihood of at least 0.5;

- the average likelihood of the four is at least 0.7; and

- the shoulder-to-hip length and the hip-to-knee length are each at least 5 pixels, and their ratio lies between 0.3 and 3.0, which rules out clustered or distorted shapes.

The first version of this check required both shoulders and both hips together with a shoulder-width ratio. Recordings made from the side showed that this rejected real people, because the far side of the body is hidden and shoulder width almost disappears in a profile view. The check was therefore changed to test each side separately, which accepts both a front view and a side view. <span class="mark">\[Fill in: the result of re-testing the side view and the pillow, bolster and toy check after this change.\]</span> If the check fails, the app shows "No person detected" and clears any red highlighting.

### 3.9.7 Camera Distance (Framing) Check

If the person is too close, parts of the body leave the frame, and if they are too far, the landmarks become unreliable. The app builds a bounding box around every detected landmark, measures its diagonal, and divides it by the diagonal of the camera frame. A ratio above 0.85 produces "Step back, you're too close", and a ratio below 0.30 produces "Move closer to the camera". Otherwise the frame goes on to the exercise rules. The same limits are used for all exercises, which is a known limitation because a horizontal exercise such as Plank occupies a different shape of space from a standing one.

### 3.9.8 Repetition Counting

Each exercise that counts reps is a small two-state machine. A rep is counted when the movement goes from one state to the other and back. Table 3.6 lists the signal and thresholds used. A rep is only counted if at least 300 milliseconds have passed since the previous one, which filters out detection jitter.

Table 3.6: Rep counting signals and thresholds

| **Exercise** | **Signal**                              | **Thresholds**                                                                             |
|--------------|-----------------------------------------|--------------------------------------------------------------------------------------------|
| Push-Up      | Elbow angle                             | Extended at 155 degrees or more; counted as bent at 90 degrees or less.                    |
| Squat        | Knee angle                              | Extended at 160 degrees or more; counted as bent at 100 degrees or less.                   |
| Jumping Jack | Wrist position against shoulder and hip | Open when both wrists are above the shoulders; closed when both wrists are below the hips. |
| Plank        | Not counted as reps                     | Hold time only, with calories added per minute.                                            |

### 3.9.9 Form Checks

Instead of judging a single moment, the app records the worst value of each measurement during the rep and judges the rep against it at the end. This stops a brief good position from hiding a mistake that happened earlier in the rep. Table 3.7 summarises the checks.

Table 3.7: Form checks for each exercise

| **Exercise** | **Check**      | **Rule and threshold**                                                                                   |
|--------------|----------------|----------------------------------------------------------------------------------------------------------|
| Push-Up      | Body alignment | Smallest shoulder-hip-ankle angle during the rep must be at least 160 degrees.                           |
| Push-Up      | Arm symmetry   | Largest difference between left and right elbow angles during the down phase must not exceed 20 degrees. |
| Push-Up      | Tempo          | The rep must take at least 600 milliseconds.                                                             |
| Squat        | Torso lean     | Smallest shoulder-hip-knee angle during the down phase must be at least 45 degrees.                      |
| Squat        | Leg symmetry   | Largest difference between left and right knee angles during the down phase must not exceed 20 degrees.  |
| Squat        | Tempo          | The rep must take at least 600 milliseconds.                                                             |
| Jumping Jack | Leg spread     | Ankle distance divided by hip width, at its smallest while the arms are raised, must be at least 1.4.    |
| Jumping Jack | Tempo          | The rep must take at least 600 milliseconds.                                                             |
| Plank        | Body line      | Shoulder-hip-ankle angle of at least 160 degrees is good form. Below 140 degrees is a larger fault.      |

#### 3.9.9.1 Left and Right Symmetry

When both sides of the body are visible, the app compares the left and right joint angles during the lowest part of the movement. The largest difference seen during the rep is kept, and if it is more than 20 degrees the rep is marked as uneven. The check is skipped when one side is hidden, which commonly happens when the camera is to the side of the user.

#### 3.9.9.2 Rep Tempo

The time from the start of a rep to its end is measured. A rep shorter than 600 milliseconds is marked as too fast, because it suggests the user is relying on momentum instead of controlling the movement.

#### 3.9.9.3 Plank Hip Direction

A plain angle cannot say whether the hips are too high or too low. For Plank, the app finds where the hip would sit if the body were a straight line from shoulder to ankle, and compares that with the actual hip position. If the hip is below the line by more than 15 pixels, the message says the hips are sagging and tells the user to lift them. If it is above the line by more than 15 pixels, the message says the hips are too high and tells the user to lower them. The 15 pixel dead zone stops the message from flipping back and forth because of small measurement noise. If the shoulder and ankle are almost on top of each other in the image, the direction cannot be found and a general message is used instead.

### 3.9.10 Priority of Feedback

A single rep can fail several checks, but the screen shows one message at a time. The app therefore reports one issue per rep, in a fixed order that puts safety first. Posture problems come first, then unevenness between the two sides, and then tempo. Table 3.8 shows the order for each exercise.

Table 3.8: Order of issue reporting

| **Exercise** | **Order (highest priority first)**                                   |
|--------------|----------------------------------------------------------------------|
| Push-Up      | Back not straight, then Uneven arm bend, then Rep too fast.          |
| Squat        | Leaning too far forward, then Uneven squat depth, then Rep too fast. |
| Jumping Jack | Legs not spread enough, then Rep too fast.                           |

The joints involved in the reported issue turn red on the skeleton. A consequence of reporting one issue is that lower-priority problems are undercounted in the form summary, which is noted as a limitation in Section 5.1.

### 3.9.11 Delivering the Feedback

The result of each frame is shown in the feedback card, and the same text is spoken with the phone's text-to-speech engine. Because detection runs many times a second, the voice only speaks again when the message changes, or after a short pause if the same message is still current. For each counted rep the app also records whether it was good or flagged, and keeps a tally of how often each issue occurred. These counts are saved with the workout.

### 3.9.12 Form Summary and Recommendations

After a workout, the form summary shows the number of good and flagged reps and the most frequent corrections from the tally. The recommendations page looks across all of a user's saved workouts, and needs at least three. It works out four things:

- Consistency: the number of days with a workout in the last seven.

- Focus area: the most frequent form correction across all workouts, with a written suggestion for that type of issue.

- Trend: the saved history for an exercise is split into an earlier half and a later half, and the share of good-form reps is compared. A rise or fall of more than ten percentage points is reported as improving or slipping.

- Exercise balance: an exercise that has not been done for five days or more, compared with how often the others are done, is suggested.

All of this is calculated on the phone from the user's stored records, and no outside model is used. The ten-point and five-day limits are estimates and have not been tuned on real usage data.

### 3.9.13 Calorie Estimate

Calories are a fixed amount added for each counted rep, or for each minute for a Plank hold. The figure is a rough indicator of how much was done, not a measurement of energy burned.

### 3.9.14 Assumptions and Limitations of the Design

- The thresholds in Tables 3.6 and 3.7 come from general exercise guidance and my own testing, not from a labelled reference dataset.

- The checks use a single 2D camera view, so their reliability depends on where the camera is placed. Back and torso checks work best from the side, while the left-right check needs both sides visible. Testing on a physical phone showed that good-form reps filmed from the front were flagged as faulty (Section 4.2).

- The rules only detect the problems that were written for them.

- A trained machine-learning model was planned but not completed. A data-collection mode was built to log labelled reps for that purpose (Section 5.4).

### 3.9.15 Chapter Summary

This section described the rule-based algorithm behind ZiGym. Each camera frame is checked for a trustworthy person and a sensible distance, then analysed with exercise-specific angle, symmetry and tempo rules. One issue is reported per rep in a fixed priority order, shown as text, red joints and speech, and the results feed a form summary and a history-based recommendation page. The design is simple, fast, works offline and keeps data on the device, but its thresholds are unvalidated estimates and its accuracy depends on the camera position.

---

# Chapter 4: Testing

## 4.1 Testing

I tested the app in two rounds. The first was my own testing as I built each feature — checking that a screen did what it was supposed to do, then trying to break it. The second round happened once the main features were working: I gave the app to someone who had not used it before and let them try it without any guidance from me, to see what an actual first-time user would run into.

All of this testing was done manually rather than through an automated test suite. I considered this the more practical approach given what the app actually does — a lot of its core functionality depends on a live camera feed, a person physically moving in front of it, and whether the resulting skeleton overlay looks right on screen. None of that is something I could easily simulate with a unit test; it needed a real person doing real exercises in front of a real camera.

### 4.1.1 Testing During Development

As I built each part of the app — the login flow, saving workouts to Firestore, the camera and pose detection pipeline, moving between screens — I tested it by hand as I went, rather than waiting until the end. Mostly this meant going through a screen's normal flow and then deliberately trying to break it: turning off the internet partway through, leaving fields empty, closing the camera mid-session. A couple of real bugs came out of this early on, including one where the app would crash on logout because a variable was being read without checking if it was null first, and another where a button was sending the user to the wrong tab.

### 4.1.2 Testing With an External User

This was, honestly, the more useful round of testing. I handed the app to someone outside the project and just let them use it — no walkthrough, no explanation of what to expect. They came back with a list of issues, and a few of them were things I don't think I would have caught on my own. The most significant was the pose detection model mistaking stationary objects for a person — a pillow, a bolster, even a stuffed toy on a bed all got picked up as if someone were doing push-ups, and the rep counter happily kept incrementing with nobody actually in frame. I hadn't tested for this specifically, since my own testing always had an actual person exercising. The tester also sent over a screen recording of it happening, which made it much easier to track down exactly what was going wrong frame by frame instead of just going off a written description.

Another issue that only showed up here was that new accounts with zero recorded workouts were still showing a fixed achievement count and a full week of progress bars, as if the account already had a history. That makes sense in hindsight — I had mostly been testing with an account that already had data in it, so I never actually saw what a genuinely new account looked like. The rest were smaller but still real: a sign-up form that seemed to reject matching passwords, a birthday that came out wrong, and no way to edit height, weight or any other profile detail after registering.

### 4.1.3 Summary of Issues Found

Table 6 lists the issues found across both rounds of testing, how each one was found, how serious it was, and what I did to fix it.

| **\#** | **Issue**                                                                                                                                                                                                          | **How it was found**                                                                                   | **Severity** | **How I fixed it**                                                                                                                                                                                         |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | The app crashed with a null check error when a user logged out while the Progress tab was still listening for data in the background.                                                                              | A runtime crash while I was testing the logout flow by hand.                                           | Critical     | The Progress screen was force-unwrapping the current user without checking it was still there. I replaced that with an explicit null check, the same pattern already used on other screens.                |
| 2      | The "View Progress" button after finishing a workout always opened the Home tab instead of the Progress tab.                                                                                                       | Manual navigation testing.                                                                             | Medium       | The bottom navigation widget was ignoring its own starting-tab parameter and always used a hard-coded value. It now reads the parameter.                                                                   |
| 3      | Camera frames weren't being converted into a format the pose detection model could use, so pose detection sometimes never started.                                                                                 | Debug logging at each stage of the image-conversion pipeline, to find where frames were being dropped. | High         | Corrected the image rotation and format handling so frames are converted the same way regardless of device orientation.                                                                                    |
| 4      | The build failed because a variable was used outside the method it was declared in, inside the video recording clean-up code.                                                                                      | A compiler error during a release build.                                                               | High         | Declared the variable in the correct place in all five exercise pages.                                                                                                                                     |
| 5      | The pose detection model kept treating stationary objects (a pillow, a bolster, a stuffed toy) as a person and counted reps with nobody in frame.                                                                  | External tester, backed up by a screen recording they sent me.                                         | High         | Added a stricter confidence gate: several core landmarks each have to clear a higher confidence bar, and their proportions have to look roughly like a human torso, before a pose is trusted for counting. |
| 6      | The sign-up form said "Passwords do not match" when the tester believed they'd typed the same thing, and the date-of-birth picker could quietly save a wrong date if the user didn't navigate to their birth year. | External tester.                                                                                       | Medium       | Added show/hide toggles on both password fields so the user can see what they typed, and made the date picker open on year selection with a default that's harder to accept by mistake.                    |
| 7      | The birthday message appeared on the wrong date and came back after being dismissed.                                                                                                                               | External tester.                                                                                       | Medium       | The wrong date was the same problem as issue 6. For the repeat, I saved the dismissal on the device against today's date so it survives the screen being rebuilt.                                          |
| 8      | Brand-new accounts with no workouts still showed a fixed achievement count and a full week of progress bars.                                                                                                       | External tester.                                                                                       | High         | Replaced every placeholder with figures worked out from the account's real stored workouts.                                                                                                                |
| 9      | The workout camera opened the rear camera, so people couldn't see themselves while exercising.                                                                                                                     | External tester.                                                                                       | Medium       | The camera setup now prefers the front camera and falls back to whatever's available if there isn't one.                                                                                                   |
| 10     | A new profile picture showed up on the Profile screen but not on the Home screen or the side menu.                                                                                                                 | External tester.                                                                                       | Low          | Home and the side menu now read the picture from the same live source as the Profile screen instead of a fixed placeholder image.                                                                          |
| 11     | Users couldn't change their details after signing up. Name, date of birth, height and weight were all read-only on the profile screen.                                                                             | External tester.                                                                                       | Medium       | Made those fields tappable, each opening a small edit dialog that saves to Firestore. I left email read-only, since changing it properly means re-verifying the new address.                               |
| 12     | The logo failed to load on the splash and login screens ("Asset not found") after I moved the images into subfolders.                                                                                              | Noticed while running the app on my own phone.                                                         | Low          | Updated the asset paths on both screens to point at the new folder.                                                                                                                                        |

## 4.2 Output Analysis

This section goes through what the app actually shows on screen, and whether each output correctly reflects what is really going on underneath, meaning the pose data or the records stored for the account. I have split it into the skeleton overlay, the live feedback (written and spoken), the rep and calorie tracking, the post-workout form summary, the progress dashboard, the recommendations page, a summary table of how I checked each output, and the results of a user survey. Besides my own testing, I also use screen recordings of test runs made on a physical phone, and they showed a few problems that my own testing had missed.

### 4.2.1 Skeleton Overlay Output

While a workout is running, the detected pose is drawn over the camera feed as a skeleton, so I can see straight away that tracking is actually working. When a form check picks up a specific problem, such as a sagging back during a push-up, a torso collapsing forward during a squat or legs barely spreading during a jumping jack, the relevant joints and the line joining them turn red instead of the usual green, so it is obvious at a glance which part of the body the issue is about. If the problem is a difference between the two sides, like one arm bending more than the other, both arms turn red, since it is the gap between them that is wrong. On Plank, the shoulder, hip and ankle line goes red whenever the hips drift away from a straight line.

![Skeleton overlay with correct form (all green)](figures/image20.png)

*Skeleton overlay with correct form (all green)*

![Skeleton overlay with a flagged form issue (red segment)](figures/image21.png)

*Skeleton overlay with a flagged form issue (red segment)*

When I checked this by eye, the red segment lined up with the joints the failing check actually used, and it did not light up the whole skeleton or the wrong body part. I only looked at a limited number of sets, so this is a visual check rather than a systematic one. The recordings also showed that the skeleton itself tracked the person well from the side, including during a squat. The problem in that case was not the drawing but the check that decides whether to analyse the frame at all, which I describe in Section 4.2.7.

### 4.2.2 Live Feedback and Spoken Output

Under the camera view there is a feedback card that updates as each frame is analysed, and the same text is spoken aloud so it can be heard without looking at the screen. Before any exercise-specific check runs, the app first makes sure there is a person it can trust in frame and that they are a sensible distance away, so the first messages someone sees are often about setup rather than form: "No person detected", "Step back — you're too close", or "Move closer to the camera". In the recordings these messages also appear briefly while the person walks to the phone at the start of a set and back to stop it at the end, which is expected.

Once the exercise checks are running, messages change with what is happening in the rep, such as "Lower further" on the way down, or "Keep your back straight" or "Keep your chest up" if posture slips. When a rep is counted, the message says either "Good Form! Rep counted!" or, if something was off, adds the single most important problem after it, for example "Rep counted! Keep both arms even", "Rep counted! Keep both legs even", "Rep counted! Spread your legs wider", or "Rep counted! Slow down for better control". Only one issue is reported per rep, in a fixed order of importance, which I discuss as a limitation in Section 5.1.

Plank works differently since it is a hold rather than a set of reps. Instead of one generic message, it now says which way the hips have gone: "Hips too high" with a prompt to lower them, or "Hips sagging" with a prompt to lift them, with gentler "Almost there" versions when the drift is small, and "Great form, keep holding!" when the body is straight.

![Feedback card showing a distance prompt](figures/image22.png)

*Feedback card showing a distance prompt*

![Plank feedback card showing a directional hip message](figures/image23.png)

*Plank feedback card showing a directional hip message*

### 4.2.3 Repetition Count and Calorie Estimate

Each workout screen shows a live rep count and an estimated calorie figure, updating as reps get detected. The calorie number is just a fixed amount added per rep (or per minute for a hold like Plank). It is not based on anything physiological, so it should be read as a rough sense of how much you did rather than an actual measurement of energy burned. One small inconsistency I noticed in the recordings is that the Plank result screen still shows "Total Reps 0", which does not apply to a hold, so I treat it as a cosmetic issue to tidy up.

![Workout screen showing live rep count and calorie estimate](figures/image24.png)

*Workout screen showing live rep count and calorie estimate*

### 4.2.4 Form Analysis Output

After finishing a Push-Up, Squat, or Jumping Jack session, the app shows a breakdown of how many reps were good form versus flagged, plus a list of whichever corrections came up most often in that session. That list can include uneven arm bend, uneven squat depth and reps that were too fast, alongside back alignment, forward lean and leg spread. All of this comes from measurements already worked out on the phone during the workout, and nothing about the video or images ever leaves the device to produce it. The recordings show how much this screen depends on where the camera is, which I come back to in Section 4.2.7.

![Form Analysis screen showing the good-form / issue breakdown](figures/image25.png)

*Form Analysis screen showing the good-form / issue breakdown*

### 4.2.5 Progress Dashboard Output

The progress dashboard pulls together someone's stored workouts into a weekly chart, running totals, and an achievement count based on a few fixed milestones, such as reaching a certain number of workouts or total reps. Since fixing Issue 8 from Section 4.1, all of these numbers come directly from whatever is actually stored for that account at the time the screen loads, rather than a fixed set of numbers shown to everyone.

**[TODO: Insert Figure: Progress dashboard for a new account with minimal history]**

**[TODO: Insert Figure: Progress dashboard for an account with an established history]**

### 4.2.6 Recommendations Output

This part of the app looks back across someone's entire recorded history rather than just one session. It surfaces the single most frequent form issue across all their workouts with a plain-language suggestion attached, whether their form seems to be getting better or worse over time for a given exercise, and whether they have been skipping a particular exercise compared to how often they do the others. There is a suggestion written for each type of issue the app can flag, including the newer ones (uneven sides and rushed reps). Like everything else, this runs off the data already stored for the account, computed on the device rather than through an outside model.

![Recommendations page showing the Focus Area and trend cards](figures/image27.png)

*Recommendations page showing the Focus Area and trend cards*

### 4.2.7 Output Validation Summary

Table 7 lists how I checked each output and what I found. The older rows come from my own testing. The newer rows draw on screen recordings of test runs on a physical phone: a push-up and squat set filmed from the front, a jumping jack and plank run, a squat analysis screen, and then a squat and a push-up filmed from the side.

| **Output**                                      | **How I checked it**                                                                                                                                                                                                                                                                                                                                          | **What I found**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Repetition count (Push-Up, Squat, Jumping Jack) | Counted reps myself out loud while doing sets at different speeds, then compared that to what the app showed. I also looked at the counts in the recorded runs.                                                                                                                                                                                               | The counts matched in most sets. The times they did not line up were mostly when I moved unusually fast, which the minimum-interval check is there to filter out as likely noise rather than a real rep. The recorded runs showed 5 push-ups, 4 and 2 squats (two separate runs) and 3 jumping jacks in about 42 seconds. **[TODO: Fill in: how many reps were actually performed in each run, so the counts can be compared.]**                                                                                                                                                                                                                                                                                                                                                                                             |
| Form classification (good form / flagged)       | Did sets where I deliberately kept good form, and separate sets where I deliberately did something wrong, such as rounding my back on push-ups, leaning too far forward on squats and barely moving my legs on jumping jacks, and checked whether the app agreed with what I had intended. I also looked at the form summary for the recorded good-form runs. | The result depended heavily on camera angle. In the recorded good-form runs filmed from the front, the app flagged every rep: 5 of 5 push-ups as "Back not straight" (0% good form) and 2 of 2 squats as "Uneven squat depth". These are false flags. From the front, the shoulder, hip and ankle line is foreshortened and the left and right knee angles are distorted, so the checks that need a side view or a level camera are unreliable. My own earlier sets from the side were classified correctly for the obvious cases, and borderline reps were not always consistent. **[TODO: Confirm: that this still held after the latest changes.]**                                                                                                                                                                       |
| Person-presence detection                       | Pointed the camera at a pillow, a bolster, and a stuffed toy with nobody in frame, both before and after the confidence-gate fix from Section 4.1. I later also filmed real people from the side.                                                                                                                                                             | Before the fix, several of the objects were picked up as a person, and after it none of them were. The side-view recordings then showed the opposite problem: the gate rejected real people. In the side-view squat the skeleton was drawn correctly but the card read "No person detected" for the whole set and 0 reps were counted, and the side-view push-up was rejected for most of the set. The cause was that the gate required both shoulders and both hips plus a shoulder-width ratio, and from the side the far-side landmarks are hidden and shoulder width almost disappears. I changed it to accept a confident chain of nose, shoulder, hip and knee on either side. **[TODO: Fill in: the result of repeating the side-view squat and push-up, and the pillow, bolster and toy check, after this change.]** |
| Distance-from-camera prompts                    | Stood too close to the camera and then too far back, and looked at when "Step back" and "Move closer" appeared in the recorded runs and whether they went away once the person was in a sensible position.                                                                                                                                                    | "Step back — you're too close" appeared when the phone was aimed at my torso from close range at the start and end of a set, and "Move closer to the camera" appeared once in a plank run when the person was small in the frame. Both matched where the person actually was. For most of the side-view push-up and the plank the prompts were not really tested, because the presence check rejected the frames first. **[TODO: Fill in: whether any prompt appeared when framing was fine, especially on Push-Up and Plank where the body is horizontal, after the presence-check change.]**                                                                                                                                                                                                                               |
| Uneven sides and rep speed                      | Looked at the feedback and the form summary from the recorded squat and push-up runs, and did sets with one side deliberately bending more than the other and sets done very fast versus slow.                                                                                                                                                                | From the front, the uneven-sides check fired on reps that were meant to be good form (2 of 2 squats), so at this camera position it gives false flags. From the side the check did not run, since one arm or leg is hidden, and in the recordings the presence check blocked all analysis anyway. **[TODO: Fill in: what you saw for rushed reps, and for uneven sides with a deliberate difference, once the side-view fix was in place.]**                                                                                                                                                                                                                                                                                                                                                                                 |
| Plank hip direction                             | Held a plank side-on to the camera, first with my hips too high and then letting them sag, and checked the message told me to move them the right way. The recorded plank run was also checked.                                                                                                                                                               | In the recorded plank run, "Great form, keep holding!" appeared once, but for most of the hold the card read "No person detected" even while the skeleton was drawn, because the presence check rejected a person lying face-down at an angle. The "Hips too high" and "Hips sagging" messages did not appear in the recordings. **[TODO: Fill in: a side-on plank with deliberately high and sagging hips after the presence-check change, and whether the messages came out the right way round.]**                                                                                                                                                                                                                                                                                                                        |
| Progress and achievement statistics             | Made a fresh test account, did a handful of workouts, and checked the numbers shown against what was actually stored in Firestore for that account.                                                                                                                                                                                                           | They matched, which confirmed that the placeholder-data bug from Section 4.1 (Issue 8) was actually fixed and not just patched over. **[TODO: Confirm: that you compared the screen against Firestore yourself.]**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Recommendation output                           | Used an account with a mix of good and bad reps recorded across several sessions, worked out by hand what the most common issue and the form trend should be, and compared that to what the Recommendations page showed. I also looked at a screenshot from the physical phone.                                                                               | The Focus Area card (most common push-up correction: back alignment) agreed with the push-up run in which all 5 reps were flagged "Back not straight". I also confirmed that the empty-state message shows for a brand-new account with fewer than three recorded workouts. However, the screenshot showed three things that did not agree with the rest of the app: the consistency card said 1 of the last 7 days while the Home screen showed a 2-day streak, the exercise balance card listed Push-Up, Squat and Plank as not done in a while, and the page said it was based on 10 recorded workouts while the Home screen counted 14. **[TODO: Fill in: the cause of each difference, for example whether the page only counts workouts that have form data, and whether it has been fixed.]**                         |

Taken together, the outputs that depend only on stored data, such as the progress numbers and the form summary, behaved as expected. The outputs that depend on how the person is filmed did not. The posture and left-right checks are reliable from the side and give false flags from the front, and the presence check was too strict for a side view until I changed it. That change, and the recommendation page differences above, still need to be checked on the phone. The newer checks, namely the distance prompts, the uneven-sides and tempo checks and the Plank hip direction, have had less testing than the older ones, and Section 5.1 covers what that means for how far they can be trusted.

![Form Analysis screen for a good-form push-up filmed from the front: 0% Good Form and "Back not straight" for all 5 reps](figures/image28.png)

*Form Analysis screen for a good-form push-up filmed from the front: 0% Good Form and "Back not straight" for all 5 reps*

![Side-view squat: skeleton drawn correctly but the card reads "No person detected"](figures/image29.png)

*Side-view squat: skeleton drawn correctly but the card reads "No person detected"*

### 4.2.8 User Survey Results

To get a view beyond my own testing, I asked people who had tried the app to fill in a short Google Form. It covered how easy the app was to use, how clear the instructions were, how well the skeleton overlay, rep counter and form feedback matched what they actually did, and whether they would use it again, and it also asked which exercises and camera position they used. **[TODO: Fill in: the number of respondents and how they were chosen.]**

**[TODO: Fill in: the main results, for example the average score for each rating question and the most common comments. Report separately whether people who filmed from the side rated the form feedback differently from those who filmed from the front, and describe low scores honestly.]**

![Survey Q1](figures/image30.png)

![Survey Q2](figures/image31.png)

---

# Chapter 5: Conclusion

## 5.1 Findings and Limitations

### 5.1.1 Findings

Looking back at what I ended up with, the main thing this project shows is that you can do real-time exercise form analysis on a normal phone, using an off-the-shelf pose detection model, without needing a server or any ongoing cost. A few things stood out as I built and tested it:

- The app tracks reps and gives live feedback across all five exercises, and for three of them — Push-Up, Squat, and Jumping Jack — I check several things on every rep instead of just one. On a push-up that's elbow angle, body alignment, whether both elbows are bending evenly, and how long the rep took. On a squat it's knee angle, torso lean, whether both knees are bending evenly, and tempo. On a jumping jack it's arm height, leg spread, and tempo. This mattered more than I expected — a single-angle check can't tell the difference between a rep done with good range of motion but bad form, and one done properly on every count.

- Because several things can go wrong on the same rep, I had to decide what the app says when that happens. It reports one issue per rep, in a fixed order: posture first (back alignment, torso lean), then evenness between the two sides, then tempo. I put posture first because it's the most likely to matter for safety, while the others are more about efficiency or balance. That was a deliberate design decision rather than something that fell out of the code, and I come back to its downside in the limitations.

- Plank used to give the same message whether your hips were too high or too low, which isn't much use because the fix is the opposite in each case. It now works out which way the hips have drifted, by comparing where the hip actually is to where it would sit on a straight line from shoulder to ankle, and tells you to lower or lift them accordingly.

- Before any exercise-specific check runs, the app now works out whether you're standing too close or too far from the camera and asks you to move if so. This came straight out of the camera-framing limitation I'd already run into: a badly framed shot makes every other check less reliable, so it made more sense to ask for a better position than to carry on with poor measurements.

- Testing in two stages — my own testing, then handing it to someone else entirely — caught things I don't think I'd have found otherwise, most obviously the pillow-misidentification issue and the placeholder data showing up on a brand-new account. Both got fixed, and I checked the fixes actually worked afterwards rather than just assuming they did.

- All of the form-checking logic runs on the device itself. It only ever needs the numeric landmark data the pose model already produces — nothing gets sent anywhere, so there's no ongoing cost and it works without internet.

- Beyond the live feedback during a workout, I added a recommendations feature that looks back across a user's whole workout history — their most common recurring form issue, whether their form is trending up or down over time, and whether they've been neglecting a particular exercise. It works the same way as the live checks: it's rule-based, computed from data already stored for the account, not something calling out to an external model. It also picks up the newer issue types, so if uneven sides or rushed reps turn out to be someone's most common problem, that's what it will suggest working on.

- I also added spoken feedback using the device's own text-to-speech, so corrections can be heard rather than read off the screen mid-exercise, which is obviously not always practical. I had to be careful here — pose detection runs many times a second, so without some kind of debouncing it would just repeat the same phrase constantly. It only speaks again once the feedback actually changes, or after a short pause if the same issue is still happening.

- Keeping the exercise-specific logic separate from the underlying camera and pose-detection code turned out to be a good decision in practice, not just on paper. I've added things on top several times now — the extra checks for Jumping Jack, then the evenness and tempo checks, then the distance check — and none of it needed changes to the camera or pose-detection code itself.

### 5.1.2 Limitations

There are also several things worth being upfront about, since they set real boundaries on how the system's output should be read.

- The thresholds are fixed numbers, and they don't account for people having different body proportions. Someone with different limb lengths might get judged less accurately even if their form is fine. Every one of them — the elbow and knee angles, the torso lean limit, the leg spread ratio, the 20-degree limit for uneven sides, the 600 millisecond cut-off for a rushed rep, and the distance ratios for "too close" and "too far" — was chosen from general exercise guidance, not by checking against a properly labelled reference dataset. They're reasonable starting points rather than validated values.

- Everything depends on a single 2D camera view. Some form issues are really only visible from a specific angle, so if the camera isn't positioned right for whatever's being checked, that check becomes less reliable. The Plank hip-direction check is the clearest example: it assumes the camera is side-on to the body, and if it's at an angle it could end up telling someone to lift their hips when they should lower them. It falls back to a generic message when the shoulder and ankle are almost on top of each other in the frame, but not when the angle is only slightly off.

- The check for uneven sides and the posture checks want different camera positions. Comparing left and right needs both sides of the body clearly visible, which is easiest from the front, whereas back alignment and torso lean are easiest to see from the side — and side-on is what the instructions tell people to do for push-ups and squats. From a true side view one arm or leg is often hidden behind the body, so the evenness check quietly doesn't run. I haven't found a way around this with a single camera; it's a trade-off between the two kinds of check.

- Only one issue is reported per rep. If someone's back sags and they also rush the rep, the app only tells them about the back. That's deliberate, but it means the tallies in the form summary and the recommendations undercount the lower-priority problems — someone who rushes a lot but also sags a lot might never see tempo come up as their main issue.

- Both the live checks and the recommendations only know about the specific things I told them to look for. They can't notice a form issue or a pattern I didn't think to check for, the way an actual person watching could.

- Only Push-Up, Squat, and Jumping Jack have the multi-check form analysis. Plank checks body alignment and now says which way the hips have gone, but it doesn't count reps, and Stretching only checks that someone's in frame — there isn't one geometric rule that covers every possible stretch, so I didn't try to force one.

- The distance check measures how large the person looks in the frame, and it uses the same limits for all five exercises. Someone lying in a plank or push-up takes up a very different shape of space from someone standing, so the same distance could count as fine for one exercise and too close for another. It probably needs separate limits per exercise, which I haven't worked out.

- The thresholds in the recommendations feature — the ten-point shift I used to call a trend "improving" or "slipping", and the five-day gap I used to flag a neglected exercise — are also just reasonable guesses. The app hasn't been in real use long enough to tune them against real data.

- The pose model only handles one person per frame, and it needs to see a face to get a reliable reading. I haven't tested, and the system isn't built for, more than one person being in frame at once.

- Calories are a flat estimate per rep or per minute held, not something measured from an actual physiological signal like heart rate. They're a rough indicator of how much you did, not a precise number.

- The spoken feedback only works in one language and voice right now — whatever the phone's text-to-speech engine defaults to. There's no setting in the app to change the language, voice, or how fast it talks.

- I did scope out a trained machine-learning model as an alternative to the fixed thresholds, and built the infrastructure to log labelled training data toward it. But I hadn't actually collected enough data, trained anything, or gotten a model running on-device by the time I finished this — that's genuinely future work, not something the app currently does.

Overall, I'd say the system is good at catching clear, obvious form mistakes and giving general guidance while exercising, but it isn't — and shouldn't be treated as — a precise, clinical assessment of someone's form. I go into what could address some of this in the future work section (5.4).

## 5.2 Contribution

It is worth being clear about what I actually built here versus what I used off the shelf. The pose detection itself is Google's ML Kit. I did not build or train that, and I am not claiming to have improved it. What I built is everything that turns its output into something useful for someone who is actually exercising.

- A multi-check way of judging form. Instead of one joint angle per exercise, each of the main exercises combines a check that drives the rep count with further checks on form quality, and looks at the worst point of each rep rather than a single moment. The order of priority when several checks fail at once is my own design, and it is written into the code rather than left to chance. A useful side effect is that every message the app gives can be traced back to a specific measurement I can point to, which is not true of a model that just outputs a verdict.

- Protection against bad input. The person-presence check, where several landmarks each have to be confident and plausibly human-shaped, came directly from the pillow and stuffed-toy problem my tester found. My first version required both shoulders and both hips, and recordings of side-view squats and push-ups later showed that it rejected real people because the far side of the body is hidden. I revised it to accept a confident chain of landmarks on either side. The revision is based on what I saw in the recordings and still needs to be confirmed with a retest (Section 4.2). The distance check does a similar job for framing, asking the user to reposition before any other check runs.

- Telling which way a plank has gone wrong. A plain angle cannot say whether the hips are too high or too low, because it does not have a direction. I worked around that by comparing the hip's actual position to where it would be on a straight line from shoulder to ankle, so the app can give the right advice instead of a generic one. This has had limited real-device testing so far, as explained in Section 4.2.

- Doing all of it on the device. The live feedback, the form summary and the recommendations are all worked out on the phone from landmark coordinates and the account's stored records. There is no external service and no ongoing cost, and the app handles being offline sensibly rather than just failing.

- Analysis across a user's history, not just one session. The recommendations feature looks at their most common recurring issue, whether their form is improving or slipping, and which exercises they have been neglecting, and turns that into plain-language suggestions. My device testing showed that some of its figures do not yet agree with the rest of the app, which I report in Section 4.2.

- A complete working app around the analysis. That includes recording each workout with the skeleton drawn into the video, per-user storage with a cap on how many recordings are kept, playback, a post-workout form summary, spoken feedback, a progress dashboard and an editable profile. The analysis is only useful if someone can actually use it, so I treated the surrounding app as part of the work rather than an afterthought.

- Groundwork for going further. I built a data-collection mode that logs labelled reps to a file, so a trained model could later be compared against the rules I wrote. I have not trained one yet (see Section 5.1), but the groundwork is there.

- A documented testing process that found where the rules fail. I tested in stages: my own testing, a tester who had not seen the app, screen recordings from a physical phone and a user survey. I recorded each defect, how it was found and how it was fixed (Sections 4.1 and 4.2). This showed that some of the most important problems only appear under real, unscripted use, and that the form checks depend heavily on where the camera is placed: good-form reps filmed from the front were flagged as faulty, and side-view recordings exposed the presence check problem. I consider an honest account of where the rules fail to be part of the contribution, because it shows what a later version would need to fix. **[TODO: Fill in: the number of survey respondents, if you report the survey.]**

None of this is a research contribution in the sense of a new model or a clinically validated tool, and the thresholds are estimates rather than measured values (Section 5.1). What I would point to instead is a practical one: a carefully designed set of simple, explainable rules on top of an existing pose model can give useful real-time form feedback entirely on a phone, as long as the camera is positioned properly, and I have built a working system around that idea.

## 5.3 Summary

This project set out to build a mobile fitness app, ZiGym, that watches a person exercise through the phone camera and tells them how they are doing, without needing a separate server or any paid service. I built it in Flutter, using Google's ML Kit pose detection to find the body landmarks in each camera frame and Firebase for accounts, stored workout history and video storage.

On top of the pose detection I wrote my own rule-based form analysis. It counts repetitions for Push-Up, Squat and Jumping Jack and, for each rep, checks several things instead of one: joint angles, body alignment or torso lean, whether the left and right sides are moving evenly, and how long the rep took. It also checks that the person is a sensible distance from the camera before judging anything, and for Plank it works out whether the hips are too high or sagging. Problems are shown in text, highlighted in red on the on-screen skeleton and spoken aloud, so the user does not need to look at the screen mid-exercise. After each session the app saves the results and shows a form analysis page, and a recommendations page looks across the user's history to suggest what to work on next.

Around the exercise features I built the parts a usable app needs: sign-up and login, an editable profile, a home screen with a daily challenge, progress tracking based on the user's actual workouts, a per-user limit on stored recordings, and messages that explain what is happening when the phone is offline. I also built a data collection mode so that labelled examples can be gathered for a trained model later.

I tested the app myself and then gave it to another person to try, which found problems I had not noticed, such as an object being mistaken for a person and placeholder statistics appearing on a brand-new account. I fixed these and re-checked them. The later additions, namely the distance prompts, the left and right comparison, the tempo check, the Plank hip direction and the Jumping Jack leg spread, **[TODO: Fill in: state how and when these were tested on a real device, and the outcome]**.

The system has clear limits, covered in section 5.1. Its thresholds are reasonable starting values rather than ones validated against labelled data, it relies on a single 2D camera view, and it reports one issue per rep. A trained machine-learning model is also not yet part of the app, only the means to collect data for one. I therefore see the app as a practical aid for catching clear, obvious form mistakes, not a precise assessment of someone's technique. Even so, it shows that useful real-time form feedback can run entirely on an ordinary phone at no ongoing cost, and the enhancements in section 5.4 set out how it could become more accurate and cover more exercises.

## 5.4 Future Enhancements

The current version of ZiGym does what I set out to do, but while building and testing it I kept running into things that I either ran out of time for or that would need more data than I had. I have grouped them below by what they would improve, roughly in the order I would tackle them.

### 5.4.1 Improving the Accuracy of the Form Analysis

- Train a machine-learning model on real data. This is the enhancement I would put first. I already built the data collection mode into the Push-Up, Squat and Jumping Jack pages, which logs landmark angles to a CSV file with a "good" or "bad" label chosen by the user. The next step is to collect a properly sized dataset from several different people, train a small classifier on it, convert it to TensorFlow Lite and run it on the device alongside the existing rules. A model learned from labelled examples could pick up form problems that I never wrote a rule for, which is the main thing the current rule-based approach cannot do.

- Validate and tune the thresholds. Every threshold in the app, such as the joint angles, the 20-degree limit for uneven sides, the 600 millisecond cut-off for a rushed rep and the distance ratios, is a reasonable starting value from general exercise guidance, not one checked against labelled reference data. Once I have a labelled dataset, I could measure how often each rule is right or wrong and adjust the values accordingly.

- Adapt to the individual user. Fixed thresholds treat everyone the same even though body proportions differ. A short calibration step at the start, for example a few standing frames to measure limb lengths, would let the app judge each person against their own proportions.

- Report more than one issue per rep. At the moment only the highest-priority issue is shown, which means lower-priority problems are undercounted in the form summary and the recommendations. I would like to record every issue found on a rep, and still speak only the most important one aloud so the voice feedback does not become overwhelming.

- Use separate distance limits for each exercise. The "too close" and "too far" ratios are currently shared by all five exercises, even though a person lying in a plank fills the frame very differently from someone standing. Measuring a suitable range for each exercise would make the framing prompts more reliable.

### 5.4.2 Extending Coverage to More Exercises

- Bring Plank and Stretching up to the same level as the other three exercises. Plank currently checks body alignment and the direction of any hip drift but does not combine several checks, and Stretching only confirms that a person is in frame. Plank could, for example, also check shoulder position and head alignment, and Stretching could be split into a small set of specific stretches, each with its own geometric rule.

- Add more exercises, such as lunges, sit-ups and burpees, using the same structure. Because the exercise logic is kept separate from the camera and pose-detection code, adding one should mostly mean writing a new set of rules and a new workout page.

### 5.4.3 Dealing with the Camera Limitations

- Resolve the conflict between the side view and the front view. The posture checks work best from the side, but the left and right comparison needs both sides of the body visible. Guiding the user to rotate partway through a set, or supporting two phones as two camera angles, could make both checks reliable. I have not worked out which of these is practical.

- Confirm the camera angle automatically. The Plank hip-direction check assumes the camera is side-on, and a slightly angled camera can give the wrong advice. The app could estimate the viewing angle from the relative positions of the shoulders and hips and warn the user when it is off.

- Support more than one person in frame, or at least detect it and tell the user, since the pose model currently handles a single person.

### 5.4.4 Improving the User Experience

- Add voice settings. The spoken feedback currently uses whatever language and voice the phone defaults to. A settings screen for language, voice, speed and volume, and an option to turn voice off, would make it usable by more people.

- Make the recommendations smarter. The trend and neglect thresholds in the recommendations feature are only reasonable guesses, and could be tuned once the app has been used long enough to produce real histories. Personalised weekly goals and reminders would also help keep users coming back.

- Improve the calorie estimate. Calories are currently a flat figure per rep or per minute held. Using the user's weight and height, which the profile already stores, would give a better estimate, and heart-rate data from a wearable would give a far better one.

- Allow users to change their email address, which needs the app to ask them to verify the new address again, and allow them to export or delete their workout history.

### 5.4.5 Evaluating with Real Users

Finally, the most valuable enhancement is probably the least technical one: testing with a larger and more varied group of users, including people with different body types and experience levels, and ideally with feedback from a qualified fitness instructor on whether the corrections the app gives are actually correct. That would show how well the rules hold up outside my own testing and would also supply the labelled data needed for the machine-learning model above.

---

# References

<!-- TODO: add full entries for Dwivedi et al. (2023), Topol (2019), Yadav et al. (2022), Kim & Lee (2025), Oh et al. (2023); verify author order, volume/issue and access dates flagged earlier. -->

Abhinand, G., Anas, M., Naveen Kumar, B., Radha, G., & Jituri, V. (2023). AI fitness trainer using human pose estimation. International Journal of Engineering Research & Technology, 11(8). https://www.ijert.org/research/ai-fitness-trainer-using-human-pose-estimation-IJERTCONV11IS08017.pdf

Bazarevsky, V., Grishchenko, I., Raveendran, K., Zhu, T., Zhang, F., & Grundmann, M. (2020). BlazePose: On-device real-time body pose tracking. arXiv. https://arxiv.org/abs/2006.10204

Chen, S., & Yang, R. R. (2020). Pose Trainer: Correcting exercise posture using pose estimation. arXiv. https://arxiv.org/abs/2006.11718

Collhins, B., Mitta, K., Gunawan, C., & Manalu, S. R. (2026). PoseTracker: Accuracy evaluation of AI-based mobile application for exercise posture feedback. International Journal of Computer Science and Humanitarian AI, 3(1). https://doi.org/10.21512/ijcshai.v3i1.15123

Dedhia, U., Bhoir, P., Ranka, P., & Kanani, P. (2023). Pose estimation and virtual gym assistant using MediaPipe and machine learning. IEEE Conference Proceedings. https://www.researchgate.net/publication/374786376

Firebase. (n.d.). Firebase documentation. Google. https://firebase.google.com/docs

Flutter. (n.d.). Flutter documentation. Google. https://docs.flutter.dev

Gadhvi, R., Desai, P., & Siddharth. (2025). PosePilot: An edge-AI solution for posture correction in physical exercises. arXiv. https://arxiv.org/pdf/2603.26760

Google. (2024). Pose landmarker guide. Google for Developers. https://developers.google.com/edge/mediapipe/solutions/vision/pose_landmarker

Google. (n.d.). ML Kit pose detection. Google for Developers. https://developers.google.com/ml-kit/vision/pose-detection

Haldar, C. (2026). An intelligent framework for real-time yoga pose detection and posture correction. arXiv.

Heo, S., Choi, T., & Choi, W. (2026). Clinical validation of an on-device AI-driven real-time human pose estimation and exercise prescription program: Prospective single-arm quasi-experimental study. Healthcare, 14(4), 482. https://doi.org/10.3390/healthcare14040482

Hsieh, Y. C., & Sun, Y. (2025). An intelligent mobile application to monitor and correct sitting posture using Raspberry Pi and MediaPipe pose detection. arXiv. https://arxiv.org/abs/2508.11683

Sathish, R., Sowmithran, S., Shivaprakash, S., & Lekha, S. (2025). NeuralFit: AI powered fitness application using MediaPipe with pose difference. SSRN. https://ssrn.com/abstract=5245284

Sharma, V., & Bohra, T. (2025). Posture Sense: AI-powered smart mirror for real-time exercise feedback and posture correction. SSRN. https://ssrn.com/abstract=5708522

---

# Appendices

> **TODO:** Appendix A: selected source code; Appendix B: survey questionnaire (Google Form); Appendix C: user guide. Each appendix must be referred to in the text.
