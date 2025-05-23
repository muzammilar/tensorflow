load(
    "//tensorflow:tensorflow.bzl",
    "tf_cc_test",
)
load("//tensorflow:tensorflow.default.bzl", "get_compatible_with_portable")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    licenses = ["notice"],
)

cc_library(
    name = "operator",
    srcs = [
        "operator.cc",
    ],
    hdrs = [
        "builtin_operator.h",
        "custom_operator.h",
        "operator.h",
        "simple_operator.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/lite/toco:__subpackages__",
    ],
    deps = [
        ":types",
        "//tensorflow/compiler/mlir/lite/delegates/flex:allowlisted_flex_ops_lib",
        "//tensorflow/compiler/mlir/lite/tools/versioning",
        "//tensorflow/compiler/mlir/lite/tools/versioning:op_signature",
        "//tensorflow/core:framework",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/lite/c:c_api_types",
        "//tensorflow/lite/core/c:common",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:graph_transformations",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:runtime",
        "//tensorflow/lite/toco:toco_port",
        "@com_google_absl//absl/log",
        "@com_google_absl//absl/log:check",
        "@com_google_absl//absl/memory",
        "@flatbuffers",
    ],
)

tf_cc_test(
    name = "operator_test",
    srcs = [
        "operator_test.cc",
    ],
    deps = [
        ":operator",
        "//tensorflow/core:ops",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:runtime",
        "//tensorflow/lite/toco:tooling_util",
        "@com_google_absl//absl/log:check",
        "@com_google_googletest//:gtest_main",
        "@flatbuffers",
    ],
)

cc_library(
    name = "types",
    srcs = [
        "types.cc",
    ],
    hdrs = [
        "types.h",
    ],
    compatible_with = get_compatible_with_portable(),
    deps = [
        "//tensorflow/lite:string_util",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:runtime",
        "@com_google_absl//absl/log",
        "@flatbuffers//:runtime_cc",
    ],
)

tf_cc_test(
    name = "types_test",
    srcs = [
        "types_test.cc",
    ],
    deps = [
        ":types",
        "//tensorflow/core:ops",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:runtime",
        "@com_google_googletest//:gtest_main",
        "@flatbuffers//:runtime_cc",
    ],
)

cc_library(
    name = "export",
    srcs = [
        "export.cc",
    ],
    hdrs = [
        "export.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = ["//visibility:public"],
    deps = [
        ":operator",
        ":types",
        "//tensorflow/compiler/mlir/lite/quantization/lite/toco_legacy:quantize_weights",
        "//tensorflow/compiler/mlir/lite/schema:schema_conversion_utils",
        "//tensorflow/compiler/mlir/lite/tools/versioning",
        "//tensorflow/core:lib_proto_parsing",
        "//tensorflow/core/platform:status",
        "//tensorflow/lite:schema_fbs_version",
        "//tensorflow/lite:util",
        "//tensorflow/lite/c:c_api_types",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:toco_port",
        "//tensorflow/lite/toco:tooling_util",
        "@com_google_absl//absl/log",
        "@com_google_absl//absl/strings",
        "@flatbuffers",
    ],
)

tf_cc_test(
    name = "export_test",
    srcs = [
        "export_test.cc",
    ],
    deps = [
        ":export",
        ":operator",
        ":types",
        "//tensorflow/compiler/mlir/lite/schema:schema_utils",
        "//tensorflow/core:lib_proto_parsing",
        "//tensorflow/core:ops",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "@com_google_absl//absl/log",
        "@com_google_googletest//:gtest_main",
        "@flatbuffers",
        "@local_xla//xla/tsl/protobuf:error_codes_proto_impl_cc",
    ],
)

cc_library(
    name = "import",
    srcs = [
        "import.cc",
    ],
    hdrs = [
        "import.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = ["//visibility:public"],
    deps = [
        ":operator",
        ":types",
        "//tensorflow/compiler/mlir/lite/schema:schema_utils",
        "//tensorflow/lite:framework",
        "//tensorflow/lite/core:framework",
        "//tensorflow/lite/core/tools:verifier",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:model_flags_proto_cc",
        "//tensorflow/lite/toco:tooling_util",
        "@com_google_absl//absl/log",
        "@com_google_absl//absl/log:check",
        "@flatbuffers",
    ],
)

tf_cc_test(
    name = "import_test",
    srcs = [
        "import_test.cc",
    ],
    tags = [
        "no_oss",  # TODO(b/273558651): Enable after updating flatbuffer version.
    ],
    deps = [
        ":import",
        "//tensorflow/compiler/mlir/lite/schema:schema_conversion_utils",
        "//tensorflow/core:ops",
        "//tensorflow/lite:schema_fbs_version",
        "//tensorflow/lite/schema:schema_fbs",
        "//tensorflow/lite/toco:model",
        "//tensorflow/lite/toco:model_flags_proto_cc",
        "//tensorflow/lite/toco:toco_port",
        "@com_google_googletest//:gtest_main",
        "@flatbuffers",
    ],
)
