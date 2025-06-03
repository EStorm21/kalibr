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
    visibility = ["//visibility:public"],
    copts = [
        "-std=c99",
        "-fPIC",
        "-Wall",
        "-Wno-unused-parameter",
        "-Wno-unused-function",
    ],
    linkopts = select({
        "@platforms//os:linux": ["-lpthread", "-lm"],
        "@platforms//os:macos": ["-lpthread"],
        "//conditions:default": [],
    }),
)