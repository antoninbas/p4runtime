package(
    default_visibility = [ "//visibility:public" ],
)

# load("@org_pubref_rules_protobuf//cpp:rules.bzl", "cpp_proto_library")
# load("@org_pubref_rules_protobuf//python:rules.bzl", "py_proto_compile")

# cpp_proto_library(
#     name = "status_proto_cc",
#     protos = ["google/rpc/status.proto"],
#     imports = ["external/com_google_protobuf/src/"],
#     inputs = ["@com_google_protobuf//:well_known_protos"],
#     with_grpc = False,
# )

# py_proto_compile(
#     name = "status_proto_py",
#     protos = ["google/rpc/status.proto"],
#     imports = ["external/com_google_protobuf/src/"],
#     inputs = ["@com_google_protobuf//:well_known_protos"],
#     with_grpc = False,
# )

proto_library(
    name = "status_proto",
    deps = ["@com_google_protobuf//:any_proto"],
    srcs = ["google/rpc/status.proto"],
)

proto_library(
    name = "code_proto",
    srcs = ["google/rpc/code.proto"],
)

cc_proto_library(
    name = "status_proto_cc",
    deps = [":status_proto"],
)

cc_proto_library(
    name = "code_proto_cc",
    deps = [":code_proto"],
)
