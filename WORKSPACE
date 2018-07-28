workspace(name = "com_github_p4lang_p4runtime")

# load("//bazel:deps.bzl", "p4runtime_deps")
# p4runtime_deps()
# load("//bazel:rules.bzl", "p4runtime_proto_repositories")
# p4runtime_proto_repositories()

load("//bazel:workspace_rule.bzl", "remote_workspace")

remote_workspace(
    name = "com_google_protobuf",
    remote = "https://github.com/google/protobuf",
    tag = "3.5.2",
)

remote_workspace(
    name = "com_github_grpc_grpc",
    remote = "https://github.com/p4lang/grpc",
    # tag = "1.13.1",
    commit = "1102d227a643ced05ec2f77ff1fdfe77982e2de7",
)

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()

remote_workspace(
    name = "com_github_googleapis",
    remote = "https://github.com/googleapis/googleapis",
    commit = "37cc0e5acae50ee91f00827a7010c3b07dfa5311",
    build_file = "bazel/external/googleapis.BUILD",
)
