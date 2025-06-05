package(default_visibility = ["//visibility:public"])

cc_library(
    name = "pybind11",
    hdrs = glob([
        "include/pybind11/**/*.h",
    ]),
    includes = ["include"],
    # Python headers are system-installed in Docker
)