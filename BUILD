load("@foreign_cc_platform_utils//:bazel_version.bzl", "BAZEL_VERSION")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external"
# On Bazel CI Mac machines, we are using cmake built from sources
toolchain(
    name = "cmake_toolchain",
    exec_compatible_with = [
        "@bazel_tools//platforms:osx",
        "@bazel_tools//platforms:x86_64",
    ],
    toolchain = "@rules_foreign_cc//tools/build_defs/native_tools:built_cmake",
    toolchain_type = "@rules_foreign_cc//tools/build_defs:cmake_toolchain",
)

# On Bazel CI Mac machines, we are using ninja built from sources
toolchain(
    name = "ninja_toolchain",
    exec_compatible_with = [
        "@bazel_tools//platforms:osx",
        "@bazel_tools//platforms:x86_64",
    ],
    toolchain = "@rules_foreign_cc//tools/build_defs/native_tools:built_ninja",
    toolchain_type = "@rules_foreign_cc//tools/build_defs:ninja_toolchain",
)
