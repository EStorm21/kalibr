workspace(name = "kalibr")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Bazel rules for C++
http_archive(
    name = "rules_cc",
    urls = ["https://github.com/bazelbuild/rules_cc/releases/download/0.0.9/rules_cc-0.0.9.tar.gz"],
    sha256 = "2037875b9a4456dce4a79d112a8ae885bbc4aad968e6587dca6e64f3a0900cdf",
    strip_prefix = "rules_cc-0.0.9",
)

# Bazel rules for Python
http_archive(
    name = "rules_python",
    sha256 = "84aec9e21cc56fbc7f1335035a71c850d1b9b5cc6ff497306f84cced9a769841",
    strip_prefix = "rules_python-0.23.1",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.23.1/rules_python-0.23.1.tar.gz",
)

load("@rules_python//python:repositories.bzl", "py_repositories")
py_repositories()

# Google Test
http_archive(
    name = "com_google_googletest",
    urls = ["https://github.com/google/googletest/archive/release-1.11.0.tar.gz"],
    strip_prefix = "googletest-release-1.11.0",
    sha256 = "b4870bf121ff7795ba20d20bcdd8627b8e088f2d1dab299a031c1034eddc93d5",
)

# Eigen - Using system eigen instead of downloading
new_local_repository(
    name = "eigen",
    path = "/usr/include",
    build_file_content = """
cc_library(
    name = "eigen",
    hdrs = glob([
        "eigen3/Eigen/**",
        "eigen3/unsupported/Eigen/**",
    ]),
    includes = ["eigen3"],
    visibility = ["//visibility:public"],
    defines = ["EIGEN_MPL2_ONLY"],
)
""",
)

# Boost - Using system boost instead of rules_boost to avoid compatibility issues
new_local_repository(
    name = "boost",
    path = "/usr",
    build_file_content = """
cc_library(
    name = "boost",
    srcs = glob([
        "lib/libboost_*.so*",
        "lib/libboost_*.a",
        "lib/x86_64-linux-gnu/libboost_*.so*",
        "lib/x86_64-linux-gnu/libboost_*.a",
        "lib/aarch64-linux-gnu/libboost_*.so*",
        "lib/aarch64-linux-gnu/libboost_*.a",
    ]),
    hdrs = glob([
        "include/boost/**/*.h",
        "include/boost/**/*.hpp",
        "include/boost/**/*.ipp",
    ]),
    includes = ["include"],
    visibility = ["//visibility:public"],
    linkopts = [
        "-lboost_system",
        "-lboost_filesystem", 
        "-lboost_serialization",
        "-lboost_thread",
        "-lboost_chrono",
        "-lboost_date_time",
        "-lboost_regex",
        "-lpthread",
    ],
)
""",
)

# OpenCV
# Using common Linux path - adjust if needed
new_local_repository(
    name = "opencv",
    path = "/usr",
    build_file_content = """
cc_library(
    name = "opencv",
    srcs = glob([
        "lib/libopencv_*.dylib",
        "lib/libopencv_*.so",
        "lib/libopencv_*.so.*",
        "lib/libopencv_*.a",
        "lib/x86_64-linux-gnu/libopencv_*.so",
        "lib/x86_64-linux-gnu/libopencv_*.so.*",
        "lib/x86_64-linux-gnu/libopencv_*.a",
        "lib/aarch64-linux-gnu/libopencv_*.so",
        "lib/aarch64-linux-gnu/libopencv_*.so.*",
        "lib/aarch64-linux-gnu/libopencv_*.a",
    ]),
    hdrs = glob([
        "include/opencv2/**/*.h",
        "include/opencv2/**/*.hpp",
        "include/opencv4/opencv2/**/*.h",
        "include/opencv4/opencv2/**/*.hpp",
    ]),
    includes = [
        "include",
        "include/opencv4",
    ],
    visibility = ["//visibility:public"],
    linkopts = [],
)
""",
)

# Intel TBB
http_archive(
    name = "oneTBB",
    urls = ["https://github.com/oneapi-src/oneTBB/archive/refs/tags/v2021.9.0.tar.gz"],
    strip_prefix = "oneTBB-2021.9.0",
    sha256 = "1ce48f34dada7837f510735ff1172f6e2c261b09460e3bf773b49791d247d24e",
    build_file_content = """
cc_library(
    name = "tbb",
    srcs = glob([
        "src/tbb/*.cpp",
        "src/tbb/*.h",
    ], exclude = [
        "src/tbb/*_test.cpp",
        "src/tbb/test_*.cpp",
    ]),
    hdrs = glob([
        "include/tbb/**/*.h",
        "include/oneapi/tbb/**/*.h",
    ]),
    includes = [
        "include",
    ],
    visibility = ["//visibility:public"],
    copts = [
        "-std=c++14",
        "-D__TBB_BUILD=1",
    ],
    linkopts = ["-lpthread", "-lrt"],
)
""",
)

# SuiteSparse
new_local_repository(
    name = "suitesparse",
    path = "/usr",
    build_file_content = """
cc_library(
    name = "suitesparse",
    srcs = glob([
        "lib/libcholmod*.dylib",
        "lib/libcholmod*.so",
        "lib/libcholmod*.so.*",
        "lib/libcholmod*.a",
        "lib/libspqr*.dylib",
        "lib/libspqr*.so",
        "lib/libspqr*.so.*",
        "lib/libspqr*.a",
        "lib/libamd*.dylib",
        "lib/libamd*.so",
        "lib/libamd*.so.*",
        "lib/libamd*.a",
        "lib/libcolamd*.dylib",
        "lib/libcolamd*.so",
        "lib/libcolamd*.so.*",
        "lib/libcolamd*.a",
        "lib/libcamd*.dylib",
        "lib/libcamd*.so",
        "lib/libcamd*.so.*",
        "lib/libcamd*.a",
        "lib/libccolamd*.dylib",
        "lib/libccolamd*.so",
        "lib/libccolamd*.so.*",
        "lib/libccolamd*.a",
        "lib/libsuitesparseconfig*.dylib",
        "lib/libsuitesparseconfig*.so",
        "lib/libsuitesparseconfig*.so.*",
        "lib/libsuitesparseconfig*.a",
        "lib/x86_64-linux-gnu/libcholmod*.so",
        "lib/x86_64-linux-gnu/libcholmod*.so.*",
        "lib/x86_64-linux-gnu/libspqr*.so",
        "lib/x86_64-linux-gnu/libspqr*.so.*",
        "lib/x86_64-linux-gnu/libamd*.so",
        "lib/x86_64-linux-gnu/libamd*.so.*",
        "lib/x86_64-linux-gnu/libcolamd*.so",
        "lib/x86_64-linux-gnu/libcolamd*.so.*",
        "lib/x86_64-linux-gnu/libcamd*.so",
        "lib/x86_64-linux-gnu/libcamd*.so.*",
        "lib/x86_64-linux-gnu/libccolamd*.so",
        "lib/x86_64-linux-gnu/libccolamd*.so.*",
        "lib/x86_64-linux-gnu/libsuitesparseconfig*.so",
        "lib/x86_64-linux-gnu/libsuitesparseconfig*.so.*",
        "lib/aarch64-linux-gnu/libcholmod*.so",
        "lib/aarch64-linux-gnu/libcholmod*.so.*",
        "lib/aarch64-linux-gnu/libspqr*.so",
        "lib/aarch64-linux-gnu/libspqr*.so.*",
        "lib/aarch64-linux-gnu/libamd*.so",
        "lib/aarch64-linux-gnu/libamd*.so.*",
        "lib/aarch64-linux-gnu/libcolamd*.so",
        "lib/aarch64-linux-gnu/libcolamd*.so.*",
        "lib/aarch64-linux-gnu/libcamd*.so",
        "lib/aarch64-linux-gnu/libcamd*.so.*",
        "lib/aarch64-linux-gnu/libccolamd*.so",
        "lib/aarch64-linux-gnu/libccolamd*.so.*",
        "lib/aarch64-linux-gnu/libsuitesparseconfig*.so",
        "lib/aarch64-linux-gnu/libsuitesparseconfig*.so.*",
    ]),
    hdrs = glob([
        "include/suitesparse/*.h",
        "include/*.h",
    ]),
    includes = [
        "include",
        "include/suitesparse",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "@eigen//:eigen",
    ],
)
""",
)

# Python pip dependencies setup
load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "pip_deps",
    requirements_lock = "//:requirements_lock.txt",
)

load("@pip_deps//:requirements.bzl", "install_deps")
install_deps()

# pybind11 for Python bindings
http_archive(
    name = "pybind11",
    build_file = "//third_party:pybind11.BUILD",
    strip_prefix = "pybind11-2.11.1",
    urls = ["https://github.com/pybind/pybind11/archive/v2.11.1.tar.gz"],
    sha256 = "d475978da0cdc2d43b73f30910786759d593a9d8ee05b1b6846d1eb16c6d2e0c",
)

# System Python headers
new_local_repository(
    name = "python_headers",
    path = "/usr/include/python3.8",
    build_file_content = """
cc_library(
    name = "python_headers",
    hdrs = glob(["**/*.h"]),
    includes = ["."],
    visibility = ["//visibility:public"],
)
""",
)

# NumPy headers
new_local_repository(
    name = "numpy_headers", 
    path = "/usr/lib/python3/dist-packages/numpy/core/include",
    build_file_content = """
cc_library(
    name = "numpy_headers",
    hdrs = glob(["**/*.h"]),
    includes = ["."],
    visibility = ["//visibility:public"],
)
""",
)

# AprilTag
http_archive(
    name = "apriltag",
    urls = ["https://github.com/AprilRobotics/apriltag/archive/refs/tags/v3.3.0.tar.gz"],
    strip_prefix = "apriltag-3.3.0",
    sha256 = "74fe75fecfb6f19c5c5249effcb443cdb5b7d489cf86e8af1d2b870c7207b100",
    build_file = "//third_party:apriltag.BUILD",
)
