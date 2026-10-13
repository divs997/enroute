# Models

The `.tflite` model files are not checked in (they are git-ignored). Enroute uses:

- **Custom YOLOv11** trained on our [Roboflow dataset](https://universe.roboflow.com/t-buiyt/haii) (potholes, stairs and other hazards), exported to TensorFlow Lite
- **YOLOv5** (COCO) exported to TensorFlow Lite

Use either of these:
1. **Firebase ML (default):** upload the models in the Firebase console under Machine Learning > Custom. The app fetches them with the Firebase ML Model Downloader. The names must be exactly `yolov5s` and `yolov11_custom` (see `MainActivity.kt`).
2. **Bundled:** put the `.tflite` files in `app/src/main/assets/` and load them from there.

The attempted MiDaS depth integration expects `depth_model.tflite` in `app/src/main/assets/` (see `MiDASModel.kt`).
