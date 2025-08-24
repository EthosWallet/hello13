# BUILD.bazel - Root build file for dependency confusion testing
# Place this file in the root directory of your test repository

load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")
load("@rules_java//java:defs.bzl", "java_binary", "java_library")
load("@rules_python//python:defs.bzl", "py_binary", "py_library")
load("@missing_rules_test//:defs.bzl", "custom_rule")
load("@nonexistent_rules//:build.bzl", "test_macro")

# C++ targets with missing external dependencies
cc_library(
    name = "main_lib",
    srcs = ["src/main.cc"],
    hdrs = ["src/main.h"],
    deps = [
        # These should trigger dependency confusion detection
        "@com_github_google_protobuf//:protobuf",
        "@missing_dependency_test//:core",
        "@fake_missing_repo//:utils",
        "@local_lib//:common",
        "@missing_workspace_lib//:helpers",
        "@internal_tools//:config",
        "@external_missing_lib//:api",
        "@missing_auth_lib//:auth",
        "@vulnerable_crypto//:crypto",
    ],
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "main_binary",
    srcs = ["src/main_app.cc"],
    deps = [
        ":main_lib",
        "@shared_utils//:shared",
        "@test_private_lib//:private",
        "@missing_bazel_module//:module_lib",
        "@fake_test_module//:test_utils",
    ],
)

# Java targets with missing Maven dependencies  
java_library(
    name = "java_main_lib",
    srcs = glob(["java/src/main/java/**/*.java"]),
    deps = [
        "@maven//:com_google_guava_guava",
        "@maven//:org_apache_commons_commons_lang3",
        "@maven//:com_example_missing_artifact",  # Should trigger Maven confusion
        "@maven//:org_nonexistent_fake_lib",      # Should trigger Maven confusion
        "@missing_archive_module//:java_utils",
        "@nonexistent_rules//:java_test",
    ],
    visibility = ["//visibility:public"],
)

java_binary(
    name = "java_main_app", 
    main_class = "com.example.MainApp",
    runtime_deps = [
        ":java_main_lib",
        "@local_missing_module//:runtime",
        "@internal_missing_tools//:java_tools",
    ],
)

# Python targets with missing dependencies
py_library(
    name = "python_lib",
    srcs = ["python/lib.py"],
    deps = [
        "@missing_python_rules//:py_utils",
        "@fake_py_dependencies//:common",
    ],
)

py_binary(
    name = "python_app",
    srcs = ["python/app.py"],
    main = "python/app.py",
    deps = [
        ":python_lib", 
        "@missing_dependency_test//:python_core",
    ],
)

# Custom rules from missing dependencies
custom_rule(
    name = "custom_build_test",
    srcs = ["test/custom.txt"],
    deps = [
        "@missing_rules_test//:custom_lib",
        "@nonexistent_rules//:custom_utils",
    ],
)

# Test rule using missing macro
test_macro(
    name = "macro_test",
    data = ["test/data.txt"],
    deps = ["@fake_missing_repo//:test_data"],
)

# File groups referencing missing workspace paths
filegroup(
    name = "config_files",
    srcs = glob([
        "configs/*.json",
        "configs/*.yaml", 
    ]) + [
        "//missing-workspace-path:config.template",    # Should trigger BUILD_DEP detection
        "//nonexistent-workspace-path:settings.json", # Should trigger BUILD_DEP detection  
    ],
)

# Platform-specific targets with missing dependencies
config_setting(
    name = "linux_build",
    values = {"cpu": "k8"},
)

cc_library(
    name = "platform_lib",
    srcs = ["src/platform.cc"],
    deps = select({
        ":linux_build": [
            "@missing_linux_deps//:linux_utils",
            "@fake_platform_lib//:linux_specific",
        ],
        "//conditions:default": [
            "@missing_default_deps//:default_utils",
        ],
    }),
)

# Genrule with missing tool dependencies
genrule(
    name = "generate_code",
    srcs = ["templates/code.template"],
    outs = ["generated/code.generated"],
    tools = [
        "@missing_code_generator//:generator",
        "@fake_build_tools//:codegen",
    ],
    cmd = "$(location @missing_code_generator//:generator) $< > $@",
)

# Test targets with missing test frameworks
cc_test(
    name = "unit_tests",
    srcs = ["test/unit_test.cc"],
    deps = [
        ":main_lib",
        "@missing_test_framework//:gtest",
        "@fake_testing_lib//:mock_utils",
    ],
)

# Proto library with missing protobuf dependencies
load("@missing_proto_rules//:proto.bzl", "proto_library")

proto_library(
    name = "api_proto",
    srcs = ["proto/api.proto"],
    deps = [
        "@missing_proto_deps//:common_proto",
        "@fake_proto_lib//:base_proto",
    ],
)

# Docker targets with missing container dependencies  
load("@missing_docker_rules//:docker.bzl", "container_image")

container_image(
    name = "app_image",
    base = "@missing_base_image//image",
    files = [":main_binary"],
    deps = [
        "@missing_container_deps//:runtime",
    ],
)

# Alias targets pointing to missing dependencies
alias(
    name = "main",
    actual = "@missing_main_target//:app",
)

alias(
    name = "test_runner", 
    actual = "@fake_test_runner//:runner",
)

# Toolchain with missing tool dependencies
toolchain(
    name = "custom_toolchain",
    exec_compatible_with = [
        "@platforms//cpu:x86_64",
        "@platforms//os:linux",  
    ],
    target_compatible_with = [
        "@platforms//cpu:x86_64",
    ],
    toolchain = "@missing_toolchain_impl//:toolchain",
    toolchain_type = "@missing_toolchain_type//:type",
)

# Package group with missing package references
package_group(
    name = "internal_packages",
    packages = [
        "//...",
        "@missing_internal_repo//...",
        "@fake_package_group//internal/...",
    ],
)

# Workspace status with missing status script
workspace_status_command = "@missing_status_script//:status.sh"
