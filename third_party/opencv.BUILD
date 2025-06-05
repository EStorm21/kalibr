cc_library(
    name = "opencv",
    srcs = glob([
        "lib/libopencv_*.dylib",
        "lib/libopencv_*.so",
        "lib/libopencv_*.a",
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
    linkopts = select({
        "@platforms//os:macos": ["-framework", "Accelerate"],
        "//conditions:default": [],
    }),
)