# Enroute

**Real-time hazard detection for people with disabilities, on Android.**

Enroute points the phone camera at the path ahead, detects dangerous obstacles like potholes, stairs, vehicles and people, and warns the user with high-contrast visuals and text-to-speech. We started it at TartanHacks 2024 ([enroute-tartanhacks](https://github.com/divs997/enroute-tartanhacks)) and rebuilt it as a native app in Fall 2024.

![Enroute demo](docs/demo.gif) <!-- placeholder -->

## What we built
- **Front end and UI:** an accessible Jetpack Compose interface with intro, idle, detection, alert and settings views, adjustable font size and text-to-speech alerts
- **Navigation:** the pipeline that moves users between views and surfaces alerts
- **Detection:** YOLOv5 (COCO) and a custom YOLOv11 model trained on our [Roboflow dataset](https://universe.roboflow.com/t-buiyt/haii), converted to TensorFlow Lite and served through Firebase ML
- **Bounding boxes:** drawing boxes on the camera feed and filtering out redundant ones so alerts stay clear
- **Depth (attempted):** we started integrating MiDaS depth estimation (`MiDASModel.kt`) but hit dependency conflicts we couldn't resolve

## Impact
Puts low-cost, real-time hazard awareness on a phone people already own, without special hardware.

## Tech
Kotlin, Jetpack Compose, CameraX, TensorFlow Lite / LiteRT, Firebase ML Model Downloader, YOLOv5, YOLOv11.

## Project layout
```
app/            Android app module (com.example.enroute)
gradle/         version catalog and Gradle wrapper
models/         where the .tflite models go (see models/README.md)
docs/           screenshots and demo
```

## Setup
1. Install Android Studio (Ladybug or newer) with JDK 17 and Android SDK 34.
2. Clone and open the repo root in Android Studio, or build from the command line:
   ```bash
   git clone https://github.com/divs997/enroute && cd enroute
   ./gradlew assembleDebug
   ```
3. Create a Firebase project, register the Android app `com.example.enroute`, and put your `google-services.json` in `app/` (it is git-ignored).
4. Add the models as described in [models/README.md](models/README.md). Upload `yolov5s` and `yolov11_custom` to Firebase ML.
5. Run on a physical Android device (API 24+) with a camera.

## Team
Divya Gupta ([@divs997](https://github.com/divs997)), Reya Shukla ([@barbicgem](https://github.com/barbicgem)) and Yuqi Zou.

## Credits
Built on the [MediaPipe object detection sample](https://github.com/google-ai-edge/mediapipe-samples/tree/main/examples/object_detection/android), [Realtime MiDaS Android](https://github.com/shubham0204/Realtime_MiDaS_Depth_Estimation_Android) and a real-time object detection tutorial. Earlier snapshot: [barbicgem/Enroute](https://github.com/barbicgem/Enroute).

## License
MIT
