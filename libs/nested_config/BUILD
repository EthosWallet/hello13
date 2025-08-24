load("@rules_cc//cc:defs.bzl", "cc_library")
load("@missing_proto_lib//proto:defs.bzl", "proto_library")

# Reference to the missing local repository from root WORKSPACE
cc_library(
    name = "nested_lib",
    srcs = ["lib.cc"],
    hdrs = ["lib.h"],
    deps = [
        "@missing_local_lib//core:lib",
        "@missing_proto_lib//proto:messages",
    ],
)

# GitHub repository reference that should trigger repo jacking detection
git_repository(
    name = "vulnerable_nested_repo",
    remote = "https://github.com/nonexistent/vulnerable-repo.git",
    commit = "abc123def456",
)

# Another potential typosquatting target
cc_binary(
    name = "test_binary", 
    srcs = ["main.cc"],
    deps = [
        "@potential_typosquat_package//lib:main",
        ":nested_lib",
    ],
)
