workspace(name = "zmq")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Group the sources of the library so that CMake rule have access to it
all_content = """filegroup(name = "all", srcs = glob(["**"]), visibility = ["//visibility:public"])"""

# Rule repository
http_archive(
   name = "rules_foreign_cc",
   strip_prefix = "rules_foreign_cc-master",
   url = "https://github.com/bazelbuild/rules_foreign_cc/archive/master.zip",
)

load("@rules_foreign_cc//:workspace_definitions.bzl", "rules_foreign_cc_dependencies")

# Call this function from the WORKSPACE file to initialize rules_foreign_cc
#  dependencies and let neccesary code generation happen
#  (Code generation is needed to support different variants of the C++ Starlark API.).
#
#  Args:
#    native_tools_toolchains: pass the toolchains for toolchain types
#      '@rules_foreign_cc//tools/build_defs:cmake_toolchain' and
#      '@rules_foreign_cc//tools/build_defs:ninja_toolchain' with the needed platform constraints.
#      If you do not pass anything, registered default toolchains will be selected (see below).
#  
#    register_default_tools: if True, the cmake and ninja toolchains, calling corresponding
#      preinstalled binaries by name (cmake, ninja) will be registered after
#      'native_tools_toolchains' without any platform constraints.
#      The default is True.
rules_foreign_cc_dependencies()

http_archive(
   name = "zeromq",
   build_file_content = all_content,
   strip_prefix = "libzmq-d0d23446f5797364c885c7fdc982e5a1efe616fa",
   urls = ["https://github.com/zeromq/libzmq/archive/d0d23446f5797364c885c7fdc982e5a1efe616fa.zip"],
)
# libzmq source code repository
http_archive(
   name = "czmq",
   build_file_content = all_content,
   strip_prefix = "czmq-afc815eadb708ad34d9b01b88aa5f86528017f63",
   urls = ["https://github.com/zeromq/czmq/archive/afc815eadb708ad34d9b01b88aa5f86528017f63.zip"]
)

git_repository(
	name="zmq-bazel",
	commit = "6d50b921567f443f785b816a8d687aad1fd74e2d",
	remote = "https://github.com/amitsudharshan/zmq-bazel"
)
