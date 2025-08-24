workspace(name = "test_repo")

# This should trigger a vulnerability - local_repository pointing to missing path
local_repository(
    name = "missing_local_lib",
    path = "../non_existent_lib",
)

# This should also trigger a vulnerability - new_local_repository pointing to missing path
new_local_repository(
    name = "missing_proto_lib", 
    path = "./libs/missing_protos",
    build_file = "BUILD.missing_protos",
)

# Valid local repository that exists (should not trigger vulnerability)
local_repository(
    name = "existing_lib",
    path = "./existing_lib",
)

# Git repository (this is for testing other detection patterns)
git_repository(
    name = "external_repo",
    remote = "https://github.com/example/external-repo.git",
    tag = "v1.0.0",
)

# HTTP archive with GitHub URL
http_archive(
    name = "some_archive",
    url = "https://github.com/example/some-archive/archive/v2.0.tar.gz",
    strip_prefix = "some-archive-2.0",
)

# bazel_dep for dependency confusion testing
bazel_dep(name = "potential_typosquat_package")
bazel_dep(name = "missing_package_test")
