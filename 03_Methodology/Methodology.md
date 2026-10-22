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

## References

Firebase. (n.d.). Firebase documentation. Google. https://firebase.google.com/docs

Flutter. (n.d.). Flutter documentation. Google. https://docs.flutter.dev

Google. (2024). Pose landmarker guide. Google for Developers. https://developers.google.com/edge/mediapipe/solutions/vision/pose_landmarker

Google. (n.d.). ML Kit pose detection. Google for Developers. https://developers.google.com/ml-kit/vision/pose-detection

<!-- NOTE: non-functional requirement "Offline capability" (3.4.2) says workouts are saved when the connection is restored. Update it to match the final offline behaviour once you have tested airplane mode. -->
