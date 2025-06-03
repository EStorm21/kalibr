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