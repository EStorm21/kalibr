# Building Kalibr with Bazel

This repository has been converted to support Bazel as a build system.

## Prerequisites

1. Install Bazel (https://bazel.build/install)
2. Install system dependencies:
   - OpenCV
   - SuiteSparse
   - Python 3.x with pip

On macOS with Homebrew:
```bash
brew install opencv suite-sparse python3
```

On Ubuntu:
```bash
sudo apt-get install libopencv-dev libsuitesparse-dev python3-dev python3-pip
```

## Building

### Build all targets:
```bash
bazel build //...
```

### Build specific calibration tools:
```bash
# Camera calibration
bazel build //aslam_offline_calibration/kalibr:kalibr_calibrate_cameras

# IMU-Camera calibration
bazel build //aslam_offline_calibration/kalibr:kalibr_calibrate_imu_camera

# Rolling shutter camera calibration
bazel build //aslam_offline_calibration/kalibr:kalibr_calibrate_rs_cameras
```

### Using convenience aliases:
```bash
bazel build //:calibrate_cameras
bazel build //:calibrate_imu_camera
bazel build //:calibrate_rs_cameras
bazel build //:create_target_pdf
```

## Running

### Run calibration tools:
```bash
# Camera calibration
bazel run //:calibrate_cameras -- --bag /path/to/your/bag --target /path/to/target.yaml --models pinhole-radtan pinhole-radtan

# IMU-Camera calibration
bazel run //:calibrate_imu_camera -- --bag /path/to/your/bag --cam /path/to/cam.yaml --imu /path/to/imu.yaml --target /path/to/target.yaml
```

### Run tests:
```bash
# Run all tests
bazel test //:all_tests

# Run specific test
bazel test //Schweizer-Messer/sm_eigen:sm_eigen_test
```

## Python Dependencies

Python dependencies are managed through requirements_lock.txt. To update dependencies:

1. Edit requirements_lock.txt
2. Run `bazel clean` to ensure pip dependencies are refreshed

## Notes

1. The WORKSPACE file assumes OpenCV and SuiteSparse are installed in `/opt/homebrew` on macOS. Adjust the paths in WORKSPACE if your installation differs.

2. Some packages use auto-generated code (e.g., numpy_eigen, aslam_cv_serialization). The current BUILD files assume these files are pre-generated. For a production setup, you may want to add proper code generation rules.

3. The build configuration uses C++14 by default. This can be changed in .bazelrc if needed.

## Testing the Build

### Quick Test (No Dependencies Required)
```bash
# Minimal test to verify Bazel structure
python3 test_minimal.py
```

### Local Testing (Dependencies Required)
```bash
# Basic build test
./test_bazel_build.sh

# Full build and test
./test_bazel_build.sh --full
```

### Docker Testing (Recommended)
```bash
# Build and test in Docker
docker build -f Dockerfile.bazel -t kalibr-bazel .

# Or use docker-compose for development
docker-compose up -d kalibr-bazel
docker-compose exec kalibr-bazel bash

# Inside the container
cd /kalibr
./test_bazel_build.sh
```

## Troubleshooting

If you encounter issues:

1. Ensure all system dependencies are installed
2. Check that paths in WORKSPACE match your system
3. Run `bazel clean --expunge` and rebuild
4. Check the specific BUILD file for any TODO comments about missing functionality
5. Use Docker for a clean environment test