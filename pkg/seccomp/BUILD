package(licenses = ["notice"])  # Apache 2.0

load("//tools/go_stateify:defs.bzl", "go_library", "go_test")
load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_embed_data")

go_binary(
    name = "victim",
    testonly = 1,
    srcs = ["seccomp_test_victim.go"],
    deps = [":seccomp"],
)

go_embed_data(
    name = "victim_data",
    testonly = 1,
    src = "victim",
    package = "seccomp",
    var = "victimData",
)

go_library(
    name = "seccomp",
    srcs = [
        "seccomp.go",
        "seccomp_rules.go",
        "seccomp_unsafe.go",
    ],
    importpath = "gvisor.googlesource.com/gvisor/pkg/seccomp",
    visibility = ["//visibility:public"],
    deps = [
        "//pkg/abi/linux",
        "//pkg/bpf",
        "//pkg/log",
    ],
)

go_test(
    name = "seccomp_test",
    size = "small",
    srcs = [
        "seccomp_test.go",
        ":victim_data",
    ],
    embed = [":seccomp"],
    deps = [
        "//pkg/abi/linux",
        "//pkg/binary",
        "//pkg/bpf",
    ],
)
