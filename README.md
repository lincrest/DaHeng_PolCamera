# DaHeng_PolCamera

A real-time CUDA-accelerated DoFP polarization imaging toolkit for Daheng industrial polarization cameras.

DaHeng_PolCamera provides real-time image acquisition, polarization demosaicing, Stokes parameter reconstruction, DoLP/AoLP computation, visualization, and image saving for Division-of-Focal-Plane (DoFP) polarization cameras.

The project is currently developed and tested with the **Daheng MER2-502-79U3M POL** polarization camera.

---

## Real-time Demo

In our test environment, the CUDA-accelerated polarization processing pipeline achieves approximately **59 FPS**, with real-time performance comparable to the official Daheng GalaxyView DoFP display.

![Real-time Demo](https://raw.githubusercontent.com/Gutsfig/DaHeng_PolCamera/main/img/tupian.jpg)

---

## Features

* Real-time image acquisition using Daheng GalaxySDK
* CUDA-accelerated DoFP polarization demosaicing
* Reconstruction of four polarization intensity images:

  * I0
  * I45
  * I90
  * I135
* Stokes parameter reconstruction:

  * S0
  * S1
  * S2
* Real-time Degree of Linear Polarization (DoLP) calculation
* Real-time Angle of Linear Polarization (AoLP) calculation
* OpenCV-based real-time visualization
* Multi-threaded acquisition, processing, display, and image saving
* GPU-accelerated processing
* Approximately 59 FPS on the tested hardware platform

---

## Overview

DaHeng_PolCamera is an open-source real-time polarization imaging toolkit developed for Daheng DoFP polarization cameras.

A DoFP polarization sensor integrates micro-polarizers with different orientations directly on top of the image sensor. A typical 2 × 2 polarization super-pixel contains four polarization orientations:

* 0°
* 45°
* 90°
* 135°

The raw polarization image therefore requires polarization demosaicing before the four directional intensity images can be reconstructed.

This project performs the major polarization processing stages in real time using CUDA and OpenCV.

The main processing pipeline is:

```text
DoFP RAW Image
      ↓
Polarization Demosaicing
      ↓
I0 / I45 / I90 / I135
      ↓
Stokes Reconstruction
      ↓
S0 / S1 / S2
      ↓
DoLP / AoLP
      ↓
Real-time Visualization
      ↓
Image Saving
```

---

## Overall Processing Flowchart

The overall software workflow includes camera initialization, image acquisition, CUDA-based polarization processing, real-time display, and image saving.

![Overall Flowchart](https://raw.githubusercontent.com/Gutsfig/DaHeng_PolCamera/main/img/xiangji.jpg)

---

## Polarization Demosaicing

The project demosaics raw polarization images captured using a DoFP polarization image sensor, such as the Sony [IMX250MZR/MYR](https://www.sony-semicon.com/en/products/is/industry/polarization.html).

A polarization sensor samples different polarization orientations at neighboring pixels. The raw mosaic therefore needs to be reconstructed into four full-resolution polarization intensity images.

![Polarization Demosaicing](https://raw.githubusercontent.com/Gutsfig/DaHeng_PolCamera/main/img/masaike.jpg)

The reconstructed polarization intensity images are:

```text
I0
I45
I90
I135
```

The corresponding Stokes parameters are calculated as:

```text
S0 = I0 + I90

S1 = I0 - I90

S2 = I45 - I135
```

The Degree of Linear Polarization is calculated as:

```text
DoLP = sqrt(S1² + S2²) / S0
```

The Angle of Linear Polarization is calculated as:

```text
AoLP = 0.5 × atan2(S2, S1)
```

---

## Supported Hardware

The project has been tested with:

* Daheng MER2-502-79U3M POL
* Sony IMX250MZR/MYR-based DoFP polarization sensors
* NVIDIA CUDA-capable GPUs

Other Daheng cameras using similar DoFP polarization sensors may also be compatible, but have not yet been fully tested.

---

## Requirements

The current implementation is primarily developed for Windows.

Recommended environment:

* Windows 10 / Windows 11
* Microsoft Visual Studio 2019
* OpenCV 4.9
* CUDA 11.8
* Daheng GalaxySDK
* CMake
* NVIDIA CUDA-capable GPU

The project uses UTF-8 encoding.

---

## Tested Platform

The real-time performance shown in this repository was measured on the following platform:

* GPU: NVIDIA GeForce RTX 4070 Laptop GPU
* CPU: Intel Core i7-12800HX
* CUDA: 11.8
* OpenCV: 4.9
* Compiler: Microsoft Visual Studio 2019
* Camera SDK: Daheng GalaxySDK

On this platform, the real-time polarization processing pipeline reaches approximately **59 FPS**.

Actual performance may vary depending on camera resolution, exposure settings, GPU performance, processing configuration, and system load.

---

## Main Technologies

### CUDA Acceleration

CUDA is used to accelerate polarization image demosaicing and related image-processing operations.

Compared with CPU-only implementations, GPU acceleration significantly improves the processing speed and enables real-time polarization reconstruction.

### Multi-threaded Processing

The program uses multiple threads for different tasks, including:

```text
Camera Acquisition
        ↓
Image Processing
        ↓
Real-time Display
        ↓
Image Saving
```

This design allows image acquisition, processing, visualization, and saving to run simultaneously.

### OpenCV Visualization

OpenCV is used for real-time visualization of polarization intensity images and derived polarization information.

The program can display:

* I0
* I45
* I90
* I135
* S0
* S1
* S2
* DoLP
* AoLP

---

## Build

The general build procedure is:

1. Install Daheng GalaxySDK.
2. Install CUDA 11.8.
3. Install OpenCV 4.9.
4. Install Microsoft Visual Studio 2019.
5. Configure the GalaxySDK, CUDA, and OpenCV include/library paths.
6. Build the project using Visual Studio or CMake.
7. Connect the supported polarization camera.
8. Run the generated executable.

Detailed build instructions will be continuously improved in future releases.

---

## Prebuilt Dependencies

For convenience, some prebuilt DLL and LIB files used in the development environment are available through:

[Baidu Cloud Drive](https://pan.baidu.com/s/1qrs5XHToBmhPT8ikiA9_NA?pwd=f956)

Place the required DLL files in the same directory as the generated executable (`.exe`) file.

> Note: Third-party SDKs and libraries remain subject to their respective licenses. Users are recommended to obtain Daheng GalaxySDK and other third-party dependencies from their official sources when possible.

---

## Project Structure

A simplified structure of this repository is:

```text
DaHeng_PolCamera/
│
├── cuda_utils/
│   └── CUDA-related polarization processing code
│
├── include/
│   └── Header files
│
├── lib/
│   └── Required library files
│
├── src/
│   └── Main source code
│
├── img/
│   └── README figures and demo images
│
└── README.md
```

---

## Roadmap

* [x] Daheng camera initialization and acquisition
* [x] Real-time image display
* [x] CUDA-based polarization demosaicing
* [x] Reconstruction of I0 / I45 / I90 / I135
* [x] Stokes parameter reconstruction
* [x] Real-time DoLP computation
* [x] Real-time AoLP computation
* [x] Multi-threaded image saving
* [x] GPU-accelerated real-time processing
* [ ] Improved polarization calibration
* [ ] Non-uniformity correction
* [ ] Polarization channel response correction
* [ ] Improved DoLP/AoLP stability
* [ ] Real-time polarization correction pipeline
* [ ] Linux support
* [ ] Python interface
* [ ] More camera models
* [ ] Improved documentation and examples

---

## Applications

This project may be useful for research and development involving:

* Computational polarization imaging
* DoFP polarization cameras
* Polarization image processing
* Polarization calibration
* Material recognition
* Reflection analysis
* Object detection
* Autonomous driving
* Industrial vision
* Remote sensing
* Computer vision
* Polarization-aware ISP research

---

## Contributing

Contributions, suggestions, bug reports, and feature requests are welcome.

If you encounter a problem or would like to suggest a new feature, please open a GitHub Issue.

Pull requests are also welcome.

---

## Citation

If this project is useful for your research, you may cite or acknowledge this repository.

A formal citation format will be added in a future release.

---

## License

This project is intended for open-source research and development.

Please refer to the `LICENSE` file for detailed licensing information.

If the repository does not yet contain a `LICENSE` file, one should be added before public redistribution or reuse of the source code.

---

## Contact

For bug reports and feature requests, please use GitHub Issues.

For other inquiries, please contact:

**Email:** [907151833@qq.com](mailto:907151833@qq.com)

---

## Acknowledgements

This project uses or depends on:

* Daheng GalaxySDK
* OpenCV
* NVIDIA CUDA
* Sony DoFP polarization image sensors

Thanks to the developers and organizations that provide these technologies and tools.
