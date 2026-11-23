# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Until 0.1.0-beta.2 the package was developed in the [kubex](https://github.com/kubex-py/kubex)
repository and released together with kubex; the notes for those releases are this package's
part of kubex's changelog.

## [Unreleased]

## [0.1.0-beta.3] - 2026-11-23

### Added

- The `Programming Language :: Python :: Free Threading :: 2 - Beta` classifier: the models work on
  free-threaded Python 3.14t and 3.15t.

### Changed

- The package moved to its own repository, [kubex-py/k8s-1.37](https://github.com/kubex-py/k8s-1.37),
  with its history. The models are generated with
  [kubex-codegen](https://github.com/kubex-py/kubex-codegen) v0.2.0 from Kubernetes v1.37.2 and
  are unchanged. `pyproject.toml` and `LICENSE` are maintained by hand; `pyproject.toml` has
  project URLs for the new repository.

## [0.1.0-beta.2] - 2026-10-28

### Added

- The distribution includes the MIT `LICENSE` file.

### Fixed

- Spec-required list, map and timestamp fields accept `null` (EndpointSlice, CSINode and
  events.k8s.io Event lists).
- `CustomResourceDefinition` schema fields (`default`, `enum`, `items`, `additionalProperties`).
- `Quantity` fields accept numbers.
- The package requires `kubex-core>=0.1.0b4,<0.2` (it accepted any `kubex-core` before).

### Changed

- **Breaking:** Timestamp fields are typed `Time`/`MicroTime` and resource quantities `Quantity`
  (from `kubex_core.models.types`) instead of `datetime` and `str`.
- **Breaking:** Spec-required `Time`/`MicroTime`/byte fields are typed `T | None`. The `JSON`,
  `JSONSchemaPropsOr*`, `ManagedFieldsEntry` and `ShardInfo` modules are removed;
  `ManagedFieldsEntry` and `ShardInfo` live in `kubex_core.models.metadata`.

## [0.1.0-beta.1] - 2026-10-23

First beta, released together with kubex 0.1.0-beta.3.

### Added

- Python 3.15 support.

### Fixed

- Descriptions containing double quotes are escaped in the generated docstrings.

### Changed

- Regenerated against the Kubernetes 1.37 release spec; the alphas came from a
  pre-release spec. 109 modules are new and 17 are gone.
- The Development Status classifier is Beta.
- **Breaking:** Python 3.10 is no longer supported; the minimum is 3.11.

## [0.1.0-alpha.3] - 2026-05-12

No changes to the models; released together with kubex 0.1.0-beta.2.

## [0.1.0-alpha.2] - 2026-05-06

Released together with kubex 0.1.0-beta.1.

### Added

- `Pod` implements `HasExec`, `HasAttach`, `HasPortForward`, `HasEphemeralContainers` and
  `HasResize`, so kubex's `exec`, `attach`, `portforward`, `ephemeral_containers` and `resize`
  subresources accept it.

## [0.1.0-alpha.1] - 2026-04-19

First release: Pydantic v2 models for Kubernetes 1.37, generated from a pre-release spec.

[unreleased]: https://github.com/kubex-py/k8s-1.37/compare/v0.1.0-beta.3...HEAD
[0.1.0-beta.3]: https://github.com/kubex-py/k8s-1.37/compare/v0.1.0-beta.2...v0.1.0-beta.3
[0.1.0-beta.2]: https://github.com/kubex-py/k8s-1.37/compare/v0.1.0-beta.1...v0.1.0-beta.2
[0.1.0-beta.1]: https://github.com/kubex-py/k8s-1.37/compare/v0.1.0-alpha.3...v0.1.0-beta.1
[0.1.0-alpha.3]: https://github.com/kubex-py/k8s-1.37/compare/v0.1.0-alpha.2...v0.1.0-alpha.3
[0.1.0-alpha.2]: https://github.com/kubex-py/k8s-1.37/releases/tag/v0.1.0-alpha.2
[0.1.0-alpha.1]: https://pypi.org/project/kubex-k8s-1-37/0.1.0a1/
