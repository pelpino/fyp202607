# Diagrams

All system diagrams for ZiGym, with the section each one belongs to.

## System architecture

![Figure 3.5: System architecture](figures/image6.png)

*Figure 3.5: System architecture.* ZiGym has a client application and cloud services. Interface, camera, pose detection and form analysis all run in the Flutter app on the phone; Firebase Authentication, Cloud Firestore and Firebase Storage provide accounts, workout data and files.

## Use case diagram

![Figure 3.8: Use case diagram](figures/image17.png)

*Figure 3.8: Use case diagram.* Use cases for the user: sign up, log in, reset password, edit profile, select exercise, read instructions, perform workout, record workout, view recordings, view summary, view progress, view recommendations and log out.

## Activity diagram

![Figure 3.8.1: Activity diagram](figures/image18.png)

*Figure 3.8.1: Activity diagram.* From login to exercise selection, then for each camera frame: person and distance check, joint angles, rep counting and feedback; the workout is saved at the end.

## Class diagram

![Figure 3.8.2: Class diagram](figures/image19.jpeg)

*Figure 3.8.2: Class diagram.* Three main classes: User, Workout Session and Recording. A user has many workout sessions; a session stores exercise, reps or hold time, duration, calories, date and form issues.

## Form analysis pipeline

![Figure 3.17: Form analysis pipeline](figures/8016f1797f08e1006604d5c58518ffee59b25775.png)

*Figure 3.17: Form analysis pipeline.* Each camera frame passes the person-presence and distance checks before the exercise-specific rules run.

## Prototype development lifecycle

![Figure 3.1: Prototype development lifecycle](figures/image5.png)

*Figure 3.1: Prototype development lifecycle.* Iterative prototype methodology.

## Gantt chart (FYP1 and FYP2)

![Figure 3.2: Gantt chart (FYP1 and FYP2)](figures/image2.png)

*Figure 3.2: Gantt chart (FYP1 and FYP2).* Project schedule across both semesters.

## Literature review mind map

![Figure 2.0: Literature review mind map](figures/image4.png)

*Figure 2.0: Literature review mind map.* Topics covered in Chapter 2.

