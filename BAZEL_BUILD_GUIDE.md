# Kalibr Bazel Build Guide

This repository has been converted to support Bazel as an alternative build system to CMake.

## Prerequisites

1. Bazel 7.0.0 or later
2. System dependencies:
   - OpenCV
   - Eigen3
   - Boost
   - SuiteSparse
   - Python 3 with numpy, scipy, matplotlib
   - TBB (Threading Building Blocks)

## Building

### Build all Kalibr targets:
```bash
bazel build //aslam_offline_calibration/kalibr:all
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

## Running

### Run calibration tools:
```bash
# Camera calibration
bazel run //aslam_offline_calibration/kalibr:kalibr_calibrate_cameras -- --bag <bag_file> --topics <topics> --models <models> --target <target_yaml>

# IMU-Camera calibration
bazel run //aslam_offline_calibration/kalibr:kalibr_calibrate_imu_camera -- --bag <bag_file> --cam <cam_chain_yaml> --imu <imu_yaml> --target <target_yaml>
```

### Utility tools:
```bash
# Create calibration target PDF
bazel run //aslam_offline_calibration/kalibr:kalibr_create_target_pdf -- --type <target_type> --nx <num_x> --ny <num_y> --tsize <tag_size> --tspace <tag_spacing>

# Visualize camera calibration
bazel run //aslam_offline_calibration/kalibr:kalibr_visualize_calibration -- --cam <cam_chain_yaml>
```

## Docker Build

For a reproducible build environment, use the provided Docker setup:

```bash
# Build and test in Docker
./docker_test_build.sh

# Or manually:
docker build -f Dockerfile_ros1_20_04 -t kalibr-bazel .
docker run -it kalibr-bazel
```

## Testing

Run tests for specific packages:
```bash
# Test aslam_backend
bazel test //aslam_optimizer/aslam_backend:all

# Test camera models
bazel test //aslam_cv/aslam_cameras:all
```

## Project Structure

The Bazel build maintains the same modular structure as the original CMake build:

- `Schweizer-Messer/`: Core utility libraries (eigen, kinematics, logging, etc.)
- `aslam_cv/`: Computer vision libraries and camera models
- `aslam_optimizer/`: Optimization backend and expressions
- `aslam_nonparametric_estimation/`: Spline-based trajectory representation
- `aslam_incremental_calibration/`: Incremental calibration algorithms
- `aslam_offline_calibration/`: Main Kalibr calibration tools

## Troubleshooting

1. **Missing system dependencies**: Install required packages using your system package manager
2. **Python import errors**: Ensure Python packages are installed system-wide or in your virtual environment
3. **Build failures**: Check the verbose output with `--verbose_failures` flag

For more information, see the original Kalibr documentation.