package(default_visibility = ["//visibility:public"])

cc_library(
    name = "apriltag",
    srcs = glob([
        "*.c",
        "common/*.c",
    ]),
    hdrs = glob([
        "*.h",
        "common/*.h",
    ]),
    includes = [
        ".",
        "common",
    ],
    copts = [
        "-std=c99",
        "-fPIC",
        "-Wall",
        "-Wno-unused-parameter",
        "-Wno-unused-function",
        "-pthread",
    ],
    linkopts = ["-lm", "-pthread"],
)