load("//:distdir_deps.bzl", "gen_workspace_stanza")
load("//tools/python:private/defs.bzl", "py_library", "py_test")

package(default_visibility = ["//visibility:private"])

filegroup(
    name = "srcs",
    srcs = glob(["**"]),
    visibility = ["//src:__pkg__"],
)

filegroup(
    name = "test-deps",
    testonly = 1,
    srcs = ["//src:bazel"],
    data = [
        "//src/tools/remote:worker",
        "//src/tools/remote:worker_deploy.jar",
    ],
)

py_library(
    name = "test_base",
    testonly = 1,
    srcs = ["test_base.py"],
    data = [
        ":default_repos_stanza.txt",
        ":test-deps",
    ],
    visibility = [
        "//src/test/py/bazel:__pkg__",
        "//third_party/def_parser:__pkg__",
        "//tools/android:__pkg__",
        "//tools/build_rules:__pkg__",
        "//tools/ctexplain:__pkg__",
        "//tools/python:__pkg__",
    ],
)

gen_workspace_stanza(
    name = "default_repos_stanza",
    out = "default_repos_stanza.txt",
    repos = [
        "rules_license",
        "rules_cc",
    ],
)

py_test(
    name = "action_temp_test",
    size = "medium",
    srcs = ["action_temp_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "cc_import_test",
    size = "medium",
    srcs = ["cc_import_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "py_test",
    size = "medium",
    srcs = ["py_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "bazel_server_mode_test",
    size = "medium",
    srcs = ["bazel_server_mode_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "bazel_clean_test",
    size = "medium",
    srcs = ["bazel_clean_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "bazel_external_repository_test",
    size = "medium",
    srcs = ["bazel_external_repository_test.py"],
    data = glob(["testdata/bazel_external_repository_test/**"]),
    tags = [
        "requires-network",
    ],
    deps = [
        ":test_base",
    ],
)

py_test(
    name = "bazel_windows_test",
    size = "medium",
    srcs = select({
        "//src/conditions:windows": ["bazel_windows_test.py"],
        "//conditions:default": ["empty_test.py"],
    }),
    main = select({
        "//src/conditions:windows": "bazel_windows_test.py",
        "//conditions:default": "empty_test.py",
    }),
    deps = select({
        "//src/conditions:windows": [":test_base"],
        "//conditions:default": [],
    }),
)

py_test(
    name = "bazel_windows_symlinks_test",
    size = "medium",
    srcs = select({
        "//src/conditions:windows": ["bazel_windows_symlinks_test.py"],
        "//conditions:default": ["empty_test.py"],
    }),
    main = select({
        "//src/conditions:windows": "bazel_windows_symlinks_test.py",
        "//conditions:default": "empty_test.py",
    }),
    deps = select({
        "//src/conditions:windows": [":test_base"],
        "//conditions:default": [],
    }),
)

py_test(
    name = "windows_remote_test",
    size = "medium",
    srcs = select({
        "//src/conditions:windows": ["windows_remote_test.py"],
        "//conditions:default": ["empty_test.py"],
    }),
    main = select({
        "//src/conditions:windows": "windows_remote_test.py",
        "//conditions:default": "empty_test.py",
    }),
    deps = select({
        "//src/conditions:windows": [":test_base"],
        "//conditions:default": [],
    }),
)

py_test(
    name = "launcher_test",
    size = "medium",
    srcs = ["launcher_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "runfiles_test",
    timeout = "long",
    srcs = ["runfiles_test.py"],
    data = glob(["testdata/runfiles_test/**"]),
    deps = [
        ":test_base",
    ],
)

py_test(
    name = "runfiles_sandboxed_test",
    timeout = "long",
    srcs = ["runfiles_sandboxed_test.py"],
    data = glob(["testdata/runfiles_test/**"]),
    tags = [
        # Windows does not support sandboxing yet.
        "no_windows",
    ],
    deps = [":test_base"],
)

py_test(
    name = "bazel_windows_cpp_test",
    size = "large",
    srcs = select({
        "//src/conditions:windows": ["bazel_windows_cpp_test.py"],
        "//conditions:default": ["empty_test.py"],
    }),
    main = select({
        "//src/conditions:windows": "bazel_windows_cpp_test.py",
        "//conditions:default": "empty_test.py",
    }),
    deps = select({
        "//src/conditions:windows": [":test_base"],
        "//conditions:default": [],
    }),
)

py_test(
    name = "bazel_remote_cache_decompression_test",
    srcs = ["remote/cache_decompression_test.py"],
    main = "remote/cache_decompression_test.py",
    tags = [
        "no-sandbox",  # This test sets up mock cache on localhost.
    ],
    deps = [":test_base"],
)

py_test(
    name = "test_wrapper_test",
    srcs = select({
        "//src/conditions:windows": ["test_wrapper_test.py"],
        "//conditions:default": ["empty_test.py"],
    }),
    data = select({
        "//src/conditions:windows": [
            ":printargs",
            "native_test.bzl",
        ],
        "//conditions:default": [],
    }),
    main = select({
        "//src/conditions:windows": "test_wrapper_test.py",
        "//conditions:default": "empty_test.py",
    }),
    deps = select({
        "//src/conditions:windows": [":test_base"],
        "//conditions:default": [],
    }),
)

cc_binary(
    name = "printargs",
    testonly = 1,
    srcs = ["printargs.cc"],
)

py_test(
    name = "first_time_use_test",
    srcs = ["first_time_use_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "query_test",
    size = "medium",
    srcs = ["query_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "genrule_test",
    size = "medium",
    srcs = ["genrule_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "bazel_workspace_test",
    srcs = ["bazel_workspace_test.py"],
    deps = [":test_base"],
)

py_library(
    name = "bzlmod_test_utils",
    srcs = ["bzlmod/test_utils.py"],
)

py_test(
    name = "bazel_module_test",
    size = "large",
    srcs = ["bzlmod/bazel_module_test.py"],
    tags = [
        "requires-network",
    ],
    deps = [
        ":bzlmod_test_utils",
        ":test_base",
    ],
)

py_test(
    name = "starlark_options_test",
    srcs = ["starlark_options_test.py"],
    deps = [":test_base"],
)

py_test(
    name = "bzlmod_query_test",
    size = "large",
    srcs = ["bzlmod/bzlmod_query_test.py"],
    tags = [
        "requires-network",
    ],
    deps = [
        ":bzlmod_test_utils",
        ":test_base",
    ],
)
