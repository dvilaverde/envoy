load(
    "//bazel:envoy_build_system.bzl",
    "envoy_benchmark_test",
    "envoy_cc_benchmark_binary",
    "envoy_package",
)
load(
    "//test/extensions:extensions_build_system.bzl",
    "envoy_extension_cc_test",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_extension_cc_test(
    name = "ring_hash_lb_test",
    srcs = ["ring_hash_lb_test.cc"],
    extension_names = ["envoy.load_balancing_policies.ring_hash"],
    rbe_pool = "6gig",
    deps = [
        "//envoy/router:router_interface",
        "//source/common/network:utility_lib",
        "//source/common/upstream:upstream_includes",
        "//source/common/upstream:upstream_lib",
        "//source/extensions/load_balancing_policies/ring_hash:ring_hash_lb_lib",
        "//test/common/upstream:utility_lib",
        "//test/mocks:common_lib",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:server_factory_context_mocks",
        "//test/mocks/upstream:cluster_info_mocks",
        "//test/mocks/upstream:host_mocks",
        "//test/mocks/upstream:host_set_mocks",
        "//test/mocks/upstream:load_balancer_context_mock",
        "//test/mocks/upstream:priority_set_mocks",
        "//test/test_common:simulated_time_system_lib",
        "@envoy_api//envoy/config/cluster/v3:pkg_cc_proto",
    ],
)

envoy_extension_cc_test(
    name = "config_test",
    srcs = ["config_test.cc"],
    extension_names = ["envoy.load_balancing_policies.ring_hash"],
    rbe_pool = "6gig",
    deps = [
        "//source/extensions/load_balancing_policies/ring_hash:config",
        "//test/mocks/server:factory_context_mocks",
        "//test/mocks/upstream:cluster_info_mocks",
        "//test/mocks/upstream:priority_set_mocks",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/load_balancing_policies/ring_hash/v3:pkg_cc_proto",
    ],
)

envoy_extension_cc_test(
    name = "integration_test",
    size = "large",
    srcs = ["integration_test.cc"],
    extension_names = ["envoy.load_balancing_policies.ring_hash"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/protobuf",
        "//source/extensions/load_balancing_policies/ring_hash:config",
        "//test/integration:http_integration_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/endpoint/v3:pkg_cc_proto",
    ],
)

envoy_cc_benchmark_binary(
    name = "ring_hash_lb_benchmark",
    srcs = ["ring_hash_lb_benchmark.cc"],
    rbe_pool = "6gig",
    deps = [
        "//source/extensions/load_balancing_policies/ring_hash:ring_hash_lb_lib",
        "//test/extensions/load_balancing_policies/common:benchmark_base_tester_lib",
    ],
)

envoy_benchmark_test(
    name = "ring_hash_lb_benchmark_test",
    timeout = "long",
    benchmark_binary = "ring_hash_lb_benchmark",
)
