package(default_visibility = ["//visibility:public"])

load(
    "@io_bazel_rules_go//go:def.bzl",
    "go_binary",
    "go_library",
    "go_test",
)

genrule(
    name = "gen-config",
    srcs = [
        "config.yaml",
    ],
    outs = ["testgrid-config"],
    cmd = "$(location //testgrid/config) --yaml=$< --output=$@",
    tools = [
        "//testgrid/config",
    ],
)

go_binary(
    name = "config",
    embed = [":go_default_library"],
    importpath = "k8s.io/test-infra/testgrid/config",
)

go_test(
    name = "go_default_test",
    srcs = ["config_test.go"],
    data = [
        "config.yaml",
        "//mungegithub:submit-queue/deployment/kubernetes/configmap.yaml",
    ],
    embed = [":go_default_library"],
    importpath = "k8s.io/test-infra/testgrid/config",
    deps = [
        "//testgrid/config/yaml2proto:go_default_library",
        "//vendor/gopkg.in/yaml.v2:go_default_library",
    ],
)

go_library(
    name = "go_default_library",
    srcs = ["main.go"],
    importpath = "k8s.io/test-infra/testgrid/config",
    deps = ["//testgrid/config/yaml2proto:go_default_library"],
)

filegroup(
    name = "package-srcs",
    srcs = glob(["**"]),
    tags = ["automanaged"],
    visibility = ["//visibility:private"],
)

filegroup(
    name = "all-srcs",
    srcs = [
        ":package-srcs",
        "//testgrid/config/pb:all-srcs",
        "//testgrid/config/yaml2proto:all-srcs",
    ],
    tags = ["automanaged"],
)
