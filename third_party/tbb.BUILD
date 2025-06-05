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
    linkopts = select({
        "@platforms//os:linux": ["-lpthread", "-lrt"],
        "@platforms//os:macos": [],
        "//conditions:default": [],
    }),
)