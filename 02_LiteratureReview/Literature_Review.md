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

## References

<!-- TODO: still missing a full reference entry for Dwivedi et al. (2023), Topol (2019), Yadav et al. (2022), Kim & Lee (2025) and Oh et al. (2023). Add them or remove the in-text citations. Also verify details flagged in your FYP1 list (Abhinand author order, Collhins volume/issue, Dedhia conference/DOI, Haldar arXiv number, access dates for Firebase/Flutter/ML Kit). -->

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
