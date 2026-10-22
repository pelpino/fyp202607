# ZiGym FYP2 Progress Log

**Student:** Siew Zi Hao (QIU202407-007484) · **Supervisor:** Mr Muhamad Amirul Asyraf Rahmat · **Moderator:** Ms Yew Yean Yoong

This log is taken from the weekly progress report forms (BCS_BIT-FYP-006a). Dates in *italics* are not on a form I received and were inferred from the weekly pattern; check them.

## Timeline

| Week | Date | Main work |
|---|---|---|
| 1–3 | *TODO* | *TODO: forms not received* |
| 4 | 31 Jul 2026 | Custom painter for the ML Kit skeleton |
| 5 | 7 Aug 2026 | Testing rep counts and calories against ML Kit; false detection on objects found |
| 6 | 14 Aug 2026 | Rep and calorie data saved to Firebase; workout video recording |
| 7 | 22 Aug 2026 | Demo to supervisor: ML Kit detection, profile picture upload, saved workout videos |
| 8 | 28 Aug 2026 | APK sent to users for module testing; issues logged |
| 9 | *TODO* | *TODO: form not received* |
| 10 | *TODO* | *TODO: form not received* |
| 11 | 18 Sep 2026 | Chapters 4 and 5 started; APK sent to users for bug testing |
| 12 | 25 Sep 2026 | User testing done; good/bad form data collected; recommendations page added |
| 13 | 3 Oct 2026 | New form checks, recommendations, spoken feedback; report sections drafted |
| 14 | *TODO* | *TODO: form not received (final report, slides, demo, poster)* |

## Weekly Entries

### Week 4 — 31 Jul 2026
- **Progress:** Configured the skeleton drawing with a custom painter so ML Kit pose detection can show the posture.
- **Remarks:** Pose detection is not complete because the skeleton is incomplete.
- **Next:** Have ML Kit pose detection ready for testing by a few users, with test cases explained.

### Week 5 — 7 Aug 2026
- **Progress:** Tested ML Kit pose detection with the painted skeleton to check that rep counts and calorie calculations are correct against exercise reps and time.
- **Remarks:** Pose detection works, but reps are counted when ML Kit detects non-living objects in a similar pose. The home data is not fetched directly from Firebase. Firebase Cloud Storage needs a plan upgrade before users can upload profile pictures.
- **Next:** Prepare slides showing what changed in each module since FYP1.

### Week 6 — 14 Aug 2026
- **Progress:** Pose detection model working. Reps and calories are recorded into Firebase, and recorded video is saved in the project folder.
- **Remarks:** Accuracy still needs configuring, since non-living objects are counted as reps. The workout page needs a prompt asking whether to continue or leave and whether to save the video, instead of pausing with no command.
- **Next:** Have a few user test cases for the slides, and have the system ready for the mid-semester checkpoint.

### Week 7 — 22 Aug 2026
- **Progress:** Demo to the supervisor of the changes since FYP1: ML Kit pose detection for exercises, profile picture upload, and saving workout videos.
- **Remarks:** Slides needed covering the changes from FYP1 to FYP2 and the problems met during implementation.
- **Next:** Prepare 10 test cases. Find at least 10 respondents (students, lecturers, public) to test the app.

### Week 8 — 28 Aug 2026
- **Progress:** Flutter APK created and sent to users to test each module's status and output for errors and bugs.
- **Issues found:** password confirmation error; birthday reminder on the wrong date and reappearing; wrong birthday shown on the profile; profile cannot be modified; wrong achievements for new accounts; inaccurate human detection in workouts.
- **Next:** Fix the test case issues and justify alignment across the whole app.

### Week 11 — 18 Sep 2026
- **Progress:** Continued report Chapters 4 and 5 (testing, output analysis, findings and limitations, future enhancements). Flutter APK created and sent to users for bug testing.
- **Remarks:** User testing in progress. It is unclear whether the new posture algorithm has bugs.
- **Next:** Test and fix the new algorithm, then update the report.

### Week 12 — 25 Sep 2026
- **Progress:** User testing done. Good-form and bad-form data collected for each exercise. Recommendations page added for analysing workout data. External testing, user testing and the issue summary written up in the report.
- **Remarks:** The academic poster and Chapter 5 are still in progress.
- **Next:** Finish Chapter 5, add final app features, and complete the poster.

### Week 13 — 3 Oct 2026
- **Progress:** Extended the form analysis with a left/right symmetry check, a rep-tempo check, a camera-distance check, and a directional plank check (hips too low or too high). Finished the recommendations feature and added spoken feedback. Drafted Testing, Output Analysis, Findings and Limitations, and the Contribution section.
- **Remarks:** The symmetry check conflicts with the camera-positioning guidance: comparing left and right needs a front view, but the posture checks work best from the side, so one arm or leg is often hidden. Recorded as a limitation, not a bug. New checks should be thought through against existing design decisions before they are built.
- **Next:** Test the new checks on a physical device, resolve two file-structure questions in the code, and write the Summary and Future Enhancements sections.

### Week 14
> **TODO:** Add your week 14 entry. Suggested content from this chat: front/side-view recordings, front-view false flags (5/5 push-ups, 2/2 squats), the person-check fix for side view, offline handling, final report, slides, demo video and poster.

## Notes

- The forms are headed "BCS3105/BIT3117 Final Year Project 1" and use the earlier title "Smart gym companion: AI-based calorie management and exercise posture detection". Update to FYP2 and the ZiGym title if your template allows it.
- Week 8 listed the "inaccurate workout human detection" issue first reported in weeks 5 and 6. Its fix is described in the report (section 3.9.6).
- Weeks 1–3, 9, 10 and 14 are still blank. Send those forms and I will fill them in.
