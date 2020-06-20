load("@foreign_cc_platform_utils//:bazel_version.bzl", "BAZEL_VERSION")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

cmake_external(
   name = "zeromq_build",
   # Values to be passed as -Dkey=value on the CMake command line;
   # here are serving to provide some CMake script configuration options
   cache_entries = {
       "NOFORTRAN": "on",
       "BUILD_WITHOUT_LAPACK": "no",
   },
   lib_source = "@zeromq//:all",
shared_libraries = select({
"@bazel_tools//src/conditions:linux_x86_64": ["libzmq.so.5"],
"@bazel_tools//src/conditions:darwin" : ["libzmq.5.dylib"],
}),
 visibility = ["//visibility:public"],
)

linux_cache_entries = {
        "LIBZMQ_LIBRARIES": "$EXT_BUILD_DEPS/zeromq_build/lib/libzmq.so.5", 
	"LIBZMQ_INCLUDE_DIRS": "$EXT_BUILD_DEPS/zeromq_build/include",
}

mac_cache_entries = {
        "LIBZMQ_LIBRARIES": "$EXT_BUILD_DEPS/zeromq_build/lib",
	"LIBZMQ_INCLUDE_DIRS": "$EXT_BUILD_DEPS/zeromq_build/include",
        "CMAKE_MACOSX_RPATH": "True",
}

czmq_select = select( {
		"@bazel_tools//src/conditions:linux_x86_64": linux_cache_entries,
		"@bazel_tools//src/conditions:darwin" : mac_cache_entries},
		no_match_error="FAILED WITH NO MATCHING OS")

cmake_external(
   name = "czmq",
   # Values to be passed as -Dkey=value on the CMake command line;
   # here are serving to provide some CMake script configuration options
   cache_entries = czmq_select,
     shared_libraries = select({
    "@bazel_tools//src/conditions:linux_x86_64": ["libczmq.so.4"],
    "@bazel_tools//src/conditions:darwin" : ["libczmq.4.dylib"],
	}),

   lib_source = "@czmq//:all",
   deps=["zeromq_build"],
 visibility = ["//visibility:public"],
)

cc_binary(
    name = "testcz",
    srcs =glob(["test.c"]),
    deps=["czmq"],
)
