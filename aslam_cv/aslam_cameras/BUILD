load("@rules_cc//cc:defs.bzl", "cc_library", "cc_test")

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "aslam_cameras",
    srcs = glob(["src/*.cpp"], exclude = [
        "src/DepthCameraGeometry.cpp",  # Missing header: DepthCameraGeometry.hpp
        "src/MaskedCameraGeometry.cpp",  # Missing header: MaskedCameraGeometry.hpp
        "src/OmniCameraGeometry.cpp",   # Missing header: OmniCameraGeometry.hpp
        "src/SphericalCameraGeometry.cpp", # Missing header: SphericalCameraGeometry.hpp
        "src/PinholeRSCameraGeometry.cpp", # Missing header: PinholeRSCameraGeometry.hpp (RS = Rolling Shutter)
        "src/PinholeCameraGeometry.cpp",   # Template specialization issues - implementations in header
    ]),
    hdrs = glob([
        "include/aslam/**/*.hpp",
        "include/aslam/**/*.h",
    ]),
    includes = ["include"],
    deps = [
        "//Schweizer-Messer/sm_common",
        "//Schweizer-Messer/sm_eigen",
        "//Schweizer-Messer/sm_boost",
        "//Schweizer-Messer/sm_kinematics",
        "//Schweizer-Messer/sm_logging",
        "//Schweizer-Messer/sm_opencv",
        "//Schweizer-Messer/sm_property_tree",
        "//Schweizer-Messer/sm_random",
        "//aslam_cv/aslam_time",
        "//aslam_optimizer/aslam_backend",  # For aslam/Exceptions.hpp
        "@opencv//:opencv",
        "@eigen//:eigen",
        "@boost//:boost",
    ],
    copts = [
        "-Wall",
        "-Wextra",
        "-Wno-unused-parameter",
    ],
)

cc_test(
    name = "aslam_cameras_test",
    srcs = glob(["test/*.cpp"]),
    deps = [
        ":aslam_cameras",
        "@com_google_googletest//:gtest_main",
    ],
    copts = ["-DGTEST_USE_OWN_TR1_TUPLE=0"],
)
