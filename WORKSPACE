# Copyright 2019 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# download basic go build rules at release v0.19.3
go_build_rules_version = "0.19.3"

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "313f2c7a23fecc33023563f082f381a32b9b7254f727a7dd2d6380ccc6dfe09b",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/rules_go/releases/download/{}/rules_go-{}.tar.gz".format(go_build_rules_version, go_build_rules_version),
        "https://github.com/bazelbuild/rules_go/releases/download/{}/rules_go-{}.tar.gz".format(go_build_rules_version, go_build_rules_version),
    ],
)

# repo of protobuf
git_repository(
    name = "com_google_protobuf",
    commit = "6a59a2ad1f61d9696092f79b6d74368b4d7970a3",  # v3.9.0
    remote = "https://github.com/protocolbuffers/protobuf",
    shallow_since = "1562856725 -0700",
)

# download the rules_docker repository at release v0.9.0
rules_docker_version = "0.9.0"

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "e513c0ac6534810eb7a14bf025a0f159726753f97f74ab7863c650d26e01d677",
    strip_prefix = "rules_docker-0.9.0",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v{}/rules_docker-v{}.tar.gz".format(rules_docker_version, rules_docker_version)],
)

# download gazelle at release v0.18.1
gazelle_version = "0.18.1"

http_archive(
    name = "bazel_gazelle",
    sha256 = "be9296bfd64882e3c08e3283c58fcb461fa6dd3c171764fcc4cf322f60615a9b",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/bazel-gazelle/releases/download/{}/bazel-gazelle-{}.tar.gz".format(gazelle_version, gazelle_version),
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/{}/bazel-gazelle-{}.tar.gz".format(gazelle_version, gazelle_version),
    ],
)

# kubernetes repo infra
http_archive(
    name = "io_kubernetes_build",
    sha256 = "4a8384320fba401cbf21fef177aa113ed8fe35952ace98e00b796cac87ae7868",
    strip_prefix = "repo-infra-df02ded38f9506e5bbcbf21702034b4fef815f2f",
    urls = ["https://github.com/kubernetes/repo-infra/archive/df02ded38f9506e5bbcbf21702034b4fef815f2f.tar.gz"],
)

# bazel-skylib 0.8.0 released 2019.03.20 (https://github.com/bazelbuild/bazel-skylib/releases/tag/0.8.0)
skylib_version = "0.8.0"

http_archive(
    name = "bazel_skylib",
    sha256 = "2ef429f5d7ce7111263289644d233707dba35e39696377ebab8b0bc701f7818e",
    type = "tar.gz",
    urls = ["https://github.com/bazelbuild/bazel-skylib/releases/download/{}/bazel-skylib.{}.tar.gz".format(skylib_version, skylib_version)],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

load("@bazel_skylib//lib:versions.bzl", "versions")

versions.check(minimum_bazel_version = "0.23.0")

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(
    go_version = "1.12.7",
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

gazelle_dependencies()

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load(
    "@io_bazel_rules_docker//go:image.bzl",
    _go_image_repos = "repositories",
)

_go_image_repos()

go_repository(
    name = "com_github_golangci_golangci-lint",
    build_file_generation = "on",
    importpath = "github.com/golangci/golangci-lint",
    tag = "v1.17.1",
)

go_repository(
    name = "io_k8s_kubernetes",
    importpath = "k8s.io/kubernetes",
    tag = "v1.15.3",
)
