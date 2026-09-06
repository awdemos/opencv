# OpenCV

Open Source Computer Vision Library — a C/C++ library with Python, Java, JavaScript, and MATLAB bindings.

## Project layout

```
modules/        Core library modules
  core/         Core data structures and functions
  imgproc/      Image processing
  imgcodecs/    Image codecs
  videoio/      Video I/O
  highgui/      High-level GUI
  video/        Video analysis
  calib3d/      Camera calibration and 3D reconstruction
  features2d/   2D features framework
  objdetect/    Object detection
  ml/           Machine learning
  dnn/          Deep neural networks
  gapi/         Graph API
  python/       Python bindings
  java/         Java bindings
  js/           JavaScript / Emscripten bindings
apps/           Application modules
samples/        Code samples
data/           Test data
3rdparty/       Third-party dependencies
platforms/      Platform-specific build scripts
cmake/          CMake scripts
doc/            Documentation sources
```

## Setup commands

```bash
# Clone the repository
git clone --recursive https://github.com/awdemos/opencv.git

# Standard out-of-source CMake build
mkdir build && cd build
cmake ..
cmake --build . --parallel

# Run tests (requires building with BUILD_TESTS=ON)
cmake -D BUILD_TESTS=ON ..
cmake --build . --parallel
./bin/opencv_test_core
```

## Build/test/lint commands

```bash
# Configure with common options
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=Release \
      -D BUILD_TESTS=ON \
      -D BUILD_EXAMPLES=ON ..
cmake --build . --parallel

# Run module tests
./bin/opencv_test_core
./bin/opencv_test_imgproc
./bin/opencv_test_dnn
# (one test binary per module)

# Python smoke test
python3 -c "import cv2; print(cv2.__version__)"
```

## Key conventions

- Primary languages: C++ with C API compatibility.
- Code style follows the [OpenCV Coding Style Guide](https://github.com/opencv/opencv/wiki/Coding_Style_Guide).
- Default branch for this fork is `4.x`.
- CI workflows are stored in `.github/workflows/` but most jobs call reusable workflows from `opencv/ci-gha-workflow`.
- New functionality generally needs tests in the relevant `modules/<name>/test/` directory.
- Python bindings are generated from the C++ API and live under `modules/python/`.

## Gotchas

- This is a large upstream fork; most development happens in the upstream `opencv/opencv` repository. Verify whether a change belongs upstream first.
- CI jobs are dispatched to platform-specific reusable workflows; local reproduction of the full matrix is heavy.
- The `modules/world` module can be used to build all modules into a single library.
- contrib modules live in a separate repository (`opencv/opencv_contrib`); do not add contrib-only functionality here.
