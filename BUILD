package(
    default_visibility = ["//visibility:public"],
)

load("@com_google_protobuf//:protobuf.bzl", "internal_copied_filegroup")

P4RUNTIME_PROTO_MAP = {
    "p4types": "p4/config/v1/p4types.proto",
    "p4info": "p4/config/v1/p4info.proto",
    "p4data": "p4/v1/p4data.proto",
    "p4runtime": "p4/v1/p4runtime.proto",
}

P4RUNTIME_PROTOS = ["proto/" + s for s in P4RUNTIME_PROTO_MAP.values()]

# I originally had the BUILD file in the proto package and I was setting
# "proto_source_root" to "proto" in the proto_library rules. However it wasn't
# working because of a Bazel issue.
# See https://github.com/bazelbuild/bazel/issues/4544 for the issue
# See
# https://github.com/bazelbuild/bazel/commit/e8956648d1c94a3a51e1aba5d229d1f27bdf8e35
# for the fix.
# So instead I moved the rules to this BUILD file and I am borrowing
# internal_copied_filegroup from protobuf.bzl to "remove" the "proto" prefix
# from my paths.

internal_copied_filegroup(
    name = "_copy_protos",
    srcs = P4RUNTIME_PROTOS,
    dest = "",
    strip_prefix = "proto",
    visibility = ["//visibility:private"],
)

# load("//bazel:genproto.bzl", "cc_grpc_library")
# load("@com_github_grpc_grpc//bazel:cc_grpc_library.bzl", "cc_grpc_library")

# load("@com_google_protobuf//:protobuf.bzl", "cc_proto_library")

proto_library(
    name = "p4types_proto",
    deps = [],
    srcs = ["p4/config/v1/p4types.proto"],
)

proto_library(
    name = "p4info_proto",
    deps = [":p4types_proto", "@com_google_protobuf//:any_proto"],
    srcs = ["p4/config/v1/p4info.proto"],
)

proto_library(
    name = "p4data_proto",
    deps = [],
    srcs = ["p4/v1/p4data.proto"],
)

proto_library(
    name = "p4runtime_proto",
    deps = [":p4info_proto", ":p4data_proto",
            "@com_github_googleapis//:status_proto",
            "@com_google_protobuf//:any_proto"],
    srcs = ["p4/v1/p4runtime.proto"],
)

# [cc_proto_library(
#     name = proto + "_proto_cc",
#     deps = [proto + "_proto"],
#     ) for proto in P4RUNTIME_PROTO_MAP.keys()]

load("@com_github_grpc_grpc//bazel:cc_grpc_library.bzl", "cc_grpc_library")
# https://github.com/grpc/grpc/issues/14145
# load("//bazel:cc_grpc_library.bzl", "cc_grpc_library")

cc_grpc_library(
    name = "_p4data_grpc_cc",
    srcs = ["p4/v1/p4data.proto"],
    deps = [],
    proto_only = True,
    well_known_protos = False,
)

cc_grpc_library(
    name = "_p4types_grpc_cc",
    srcs = ["p4/config/v1/p4types.proto"],
    deps = [],
    proto_only = True,
    well_known_protos = False,
)

# cc_grpc_library issue with generated files
# https://github.com/grpc/grpc/blob/master/bazel/generate_cc.bzl#L32

cc_grpc_library(
    name = "_p4info_grpc_cc",
    srcs = ["p4/config/v1/p4info.proto"],
    deps = [":_p4types_grpc_cc"],
    proto_only = True,
    well_known_protos = True,
)

cc_grpc_library(
    name = "p4runtime_grpc_cc",
    srcs = ["p4/v1/p4runtime.proto"],
    deps = [":_p4data_grpc_cc"],
    proto_only = False,
    well_known_protos = True,
)

# cc_grpc_library(
#     name = "p4runtime_grpc_cc",
#     src = "p4/v1/p4runtime.proto",
#     # deps = [],
#     # proto_only = False,
#     # well_known_protos = "@com_google_protobuf//:well_known_protos",
# )

# TODO
# [py_proto_library(
#     name = proto + "_proto_py",
#     deps = [proto + "_proto"],
#     ) for proto in P4RUNTIME_PROTO_MAP.keys()]
