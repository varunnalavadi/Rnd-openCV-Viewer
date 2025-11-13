# 🧠 RnD OpenCV Viewer

A real-time **edge detection viewer** built for Android using **OpenCV (C++)** and **OpenGL ES 2.0**, accompanied by a lightweight **TypeScript web interface** to preview sample processed frames.

---

## 🚀 Overview

This project demonstrates an end-to-end pipeline for capturing camera frames on Android, sending them to native C++ via JNI, applying **Canny edge detection**, and rendering the results on-screen using GPU acceleration.  
A small web viewer is also provided for static visualization.

---

## 📱 Android Application

### Features
- Real-time camera feed capture using the **Camera1 API**.
- JNI bridge for passing `byte[]` camera data from Java to C++.
- Native **OpenCV** processing (Canny edge detection on the grayscale Y-plane).
- Rendering handled by **OpenGL ES 2.0**, displaying each processed frame as a texture.

### Frame Flow
1. **Camera (Java):**  
   `MainActivity.java` sets up a `PreviewCallback` that receives raw `byte[]` frame data.  
2. **JNI Bridge:**  
   Each frame calls `processFrame(int width, int height, byte[] frameData)` in native code.  
3. **C++ Layer (OpenCV):**  
   - Converts the YUV byte array into a `cv::Mat`.  
   - Extracts the luminance (Y) channel for grayscale processing.  
   - Runs `cv::Canny` on `matGray` and stores output in a global `processedMat`.  
4. **Rendering (OpenGL):**  
   - `nativeOnDrawFrame()` checks for new frames.  
   - Uploads `processedMat` as a GPU texture using `glTexImage2D`.  
   - Renders the texture on a full-screen quad.

---

## 💻 Web Viewer

A minimal **TypeScript + HTML** demo that displays a static sample frame.

- Shows `images/sample_image.jpeg` on an HTML canvas.  
- Displays mock FPS and resolution values via DOM updates.  
- Built using TypeScript and compiled to `main.js`.

---

## ⚙️ Architecture Summary

```
Camera (Java)
   ↓
JNI Bridge
   ↓
OpenCV Processing (C++)
   ↓
OpenGL Rendering (C++)
```

Each captured frame moves through this pipeline for real-time edge detection and GPU rendering.

---

## 📸 Results

**Original Image:**  
![original_image1](https://github.com/user-attachments/assets/c9b01d7b-d526-4418-92ab-bef6667c0103)



**Processed (Android App):**  
![website_image](https://github.com/user-attachments/assets/9b1d6699-c52f-4ed1-bcb1-274789e80294)



---

## 🧩 Tech Stack
- Java (Android) — Camera + JNI integration  
- C++ (NDK) — Image processing using OpenCV  
- OpenGL ES 2.0 — Real-time texture rendering  
- TypeScript + HTML — Static frame visualization

---

## ✨ Summary

**RnD-OpenCV-Viewer** demonstrates how to integrate native OpenCV image processing with Android’s camera and rendering pipeline, achieving real-time visual feedback both on-device and via a web-based viewer.

