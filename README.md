# SNHU-2026-TERM-C-5-CS-360

Module 8 Portfolio Submission — Project Three: Weight Tracker

## Project artifact

[Download the completed Android Studio source project](IlliaLevchenkoWeightTracker_ProjectThree.zip). The project contains the finalized app code and interface design. The ZIP includes the Java source, finalized XML screens, resources, and Gradle wrapper.

## App overview and user needs

The Weight Tracker helps users record and review their weight over time, set a personal target, and receive an optional text alert when a saved measurement reaches the goal threshold. It addresses the need for a simple, private way to track progress without requiring an account on an external service. Each local account has its own dated measurements, goal, display-unit choice, and messaging preferences.

## User-centered design

The app provides account creation and sign-in, a weight-entry grid with add, edit, and delete actions, goal and unit settings, and an optional SMS setup flow. The screens keep routine tracking actions direct and make the measurement history and goal easy to find. The app requests SMS access only for users who opt in; declining the permission leaves account and tracking features available. Keeping records separated by account and storing passwords as salted hashes supports privacy. The focused workflow and clear permission choice make the interface useful for both users who want alerts and those who only want to track measurements.

## Development approach

I built on the Project Two interface baseline and implemented the app in small, connected parts: screen flow and validation, SQLite persistence, account handling, goal evaluation, and SMS result handling. I used the Gradle wrapper and explicit JDK/SDK setup instructions to make the project easier to reproduce. In future work, I would continue this incremental approach, adding focused tests as each feature is implemented and validating platform integrations on representative devices.

## Testing and what it revealed

I performed a clean source build, ran lint, and exercised the app on an Android emulator. The Project Three verification record reported 16 device-suite entries passed, 0 failed, and 0 skipped; 15 executed database, goal, and screen-flow checks, while one guarded SMS entry returned without sending during the normal run. Separate checks covered both SMS permission branches: denying permission preserved weight tracking without sending a notification; granting permission produced a successful send callback and stored the notified state so the same goal alert was not sent again. The earlier verification also checked a fresh source extraction. The portfolio ZIP contains the app source and finalized interface; the test sources and verification logs are retained separately in the course materials. Testing matters because it checks both the normal user flow and conditions such as denied permissions, repeat actions, and a clean setup on another machine. The results exposed environment setup as a likely source of build friction: Java 8 and JDK 25 were incompatible with this configuration, while JDK 17 or Android Studio's JDK 21 worked. Automatic carrier delivery to a second device was not confirmed and remains a pre-release check.

## Challenge and innovation

The most challenging part was connecting the goal alert to Android's SMS permission and send-result behavior without making messaging mandatory for the app. I handled this by separating goal evaluation from the send callback, recording successful notifications to prevent duplicates, and retaining the normal save-and-track behavior when permission is denied. The result is a more resilient experience across permission choices and devices without messaging hardware.

## Skills demonstrated

The SQLite data model and account-scoped queries demonstrate my strongest work: they keep each user's goals and measurements separate while supporting the app's core add, edit, delete, and review flows. The salted password hashing, permission-aware notification logic, and device tests show how I combined security, platform behavior, and practical verification in one mobile application.

## Open and run

Extract the ZIP and open the `IlliaLevchenkoWeightTracker` folder in Android Studio. Configure Gradle to use JDK 17 or the previously verified Android Studio JDK 21, install Android SDK Platform 36 and Build-Tools 36.0.0, and allow Gradle to sync. Run the app on an API 28 or newer device or emulator. First sync requires internet access to download build dependencies. The archive omits machine-specific SDK paths and generated build output.
