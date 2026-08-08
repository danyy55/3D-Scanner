# 3D Stereo Scanner (Stardance)
<img width="3300" height="1857" alt="6e9e0cfb-73e6-4550-b769-5586c5f62120" src="https://github.com/user-attachments/assets/aefd7d8b-96e4-44b2-8ee6-b6cac1f266e1" />


An advanced, high-precision static 3D stereo scanner designed to capture objects up to 20x20x20 cm with zero moving main-parts during the optical capture phase. Built with a Raspberry Pi 5 core and hardware-triggered global shutter cameras.

## Hardware Architecture

* **Core Processor:** Raspberry Pi 5 (4GB RAM) running OpenCV in C++ for real-time 3D data computation.
* **Optical Sensors:** 2 x Arducam IMX296 1.6MP Color Global Shutter camera modules. The global shutter mechanism is critical to capture the moving laser lines without motion distortion or "jello effect."
* **Laser Projection:** Dual 520nm 15mW green line laser modules for sharp contrast and clean HSV color filtering in dark environments.
* **Scanner Enclosure:** A robust framework built using T-slot aluminum extrusions.
* **Base Platform:** A 2mm rigid styrene sheet cut into a perfect hexagonal platform providing flat, zero-reflection object placement.
* **Mirror Array:** An outer hexagon made of 6 front-surface plane mirrors tilted at precisely ~55.3° (17.3 cm width each).
* **Underbelly Capture:** A 45° W-shaped optical structure placed underneath the transparent styrene base to eliminate blind spots and seamlessly capture the object's bottom and legs.

## Software (C++ & OpenCV)

The firmware is designed to operate in low-light conditions to isolate the structural green laser lines:
1. **Exposure Control:** Manual shutter speed locking for complete noise removal.
2. **Color Segmentation:** HSV-based thresholding tuned specifically to the 520nm green light spectrum.
3. **Region Isolation:** Custom Region of Interest (ROI) masks splitting the frame into the 6 mirror segments.
4. **Point Cloud Generation:** Geometric transformation matrices and stereo triangulation algorithms projecting the visual data into a `std::vector<cv::Point3f>` point cloud.

## Repository Structure

* `/CAD` - Contains the 3D geometric assembly designs and `.STEP` structural exports.
* `/firmware` - Source code, algorithm outlines, and OpenCV main pipelines.
* `bom.csv` - The automated bill of materials tracking the budget and components.
