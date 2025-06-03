# Quick Start: Testing Kalibr with Bazel

## Option 1: Docker Development Environment (Recommended)

```bash
# Build development container (works on all architectures)
docker build -f Dockerfile.dev -t kalibr-dev .
docker run -it -v $(pwd):/kalibr kalibr-dev

# Inside container:
cd /kalibr
./test_minimal.py      # Quick structure test
./test_bazel_build.sh  # Full build test
```

## Option 1b: Docker with Pre-built (For Testing)

```bash
# This attempts a build during Docker image creation
docker build -f Dockerfile.bazelisk -t kalibr-bazel .
docker run -it kalibr-bazel

# Or use docker-compose:
docker-compose up -d kalibr-bazelisk
docker-compose exec kalibr-bazelisk bash
```

## Option 2: Local Testing (Minimal)

```bash
# Install Bazel (if not already installed)
# macOS: brew install bazel
# Ubuntu: See https://bazel.build/install/ubuntu

# Run minimal structure test (no dependencies needed)
python3 test_minimal.py

# This will verify BUILD files exist and Bazel can parse them
```

## Option 3: Local Full Build

```bash
# Install dependencies first
# macOS:
brew install opencv suite-sparse eigen boost tbb

# Ubuntu:
sudo apt-get install libopencv-dev libsuitesparse-dev libeigen3-dev \
  libboost-all-dev libtbb-dev python3-dev python3-pip

# Install Python dependencies
pip3 install -r requirements_lock.txt

# Update WORKSPACE if paths differ from defaults
# Edit opencv and suitesparse paths in WORKSPACE

# Run build test
./test_bazel_build.sh
```

## Common Issues & Fixes

1. **OpenCV/SuiteSparse not found**: Edit paths in WORKSPACE file
2. **Python import errors**: Make sure you've run `pip3 install -r requirements_lock.txt`
3. **Out of memory**: Limit parallelism with `bazel build --jobs=4 //...`
4. **Bazel cache issues**: Run `bazel clean --expunge`

## Verify It Works

Once built, test a tool:
```bash
bazel run //:calibrate_cameras -- --help
```

This should show the help text for the camera calibration tool.