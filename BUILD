# Description:
# Implementation of the Kerberos protocol from OpenJDK
load("@build_bazel_rules_android//android:rules.bzl", "android_library")

licenses(["restricted"])

exports_files(["LICENSE"])

android_library(
    name = "openjdk_kerberos",
    visibility = ["//visibility:public"],
    srcs = glob(["java/**/*.java"]),
    javacopts = ["-Xep:AndroidJdkLibsChecker:OFF"],
)
