cc_library(
    name = "aslam_imgproc",
    srcs = glob(["src/*.cpp"]),
    hdrs = glob(["include/**/*.hpp"]),
    includes = ["include"],
    deps = [
        "//aslam_cv/aslam_time:aslam_time",
        "//aslam_cv/aslam_cameras:aslam_cameras",
    ],
    visibility = ["//visibility:public"],
)
