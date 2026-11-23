# kubex-k8s-1-37

[![CI](https://github.com/kubex-py/k8s-1.37/actions/workflows/ci.yaml/badge.svg)](https://github.com/kubex-py/k8s-1.37/actions/workflows/ci.yaml)
[![PyPI](https://img.shields.io/pypi/v/kubex-k8s-1-37)](https://pypi.org/project/kubex-k8s-1-37/)

Pydantic v2 models for every Kubernetes 1.37 resource, for the [kubex](https://github.com/kubex-py/kubex)
client. They are generated from the official OpenAPI spec by
[kubex-codegen](https://github.com/kubex-py/kubex-codegen) and build on
[kubex-core](https://github.com/kubex-py/kubex-core).

```bash
pip install "kubex[k8s-1.37]"
```

```python
from kubex.api import Api
from kubex.client import create_client
from kubex.k8s.v1_37.core.v1.pod import Pod

async with await create_client() as client:
    api: Api[Pod] = Api(Pod, client=client)
    pod = await api.get("my-pod", namespace="default")
```

Documentation: https://kubex.codemageddon.me/

## How the models are made

Everything under `kubex/k8s/v1_37/` is generated. Don't edit it by hand: change
[kubex-codegen](https://github.com/kubex-py/kubex-codegen) instead. `pyproject.toml` and `LICENSE`
are written by hand; the ruff settings and the ruff and mypy versions in `pyproject.toml` match
kubex-codegen's, so CI checks the models the way they were generated.

The kubex-codegen release this repository uses is pinned in `.kubex-codegen-version`. To regenerate
from the latest 1.37.x spec:

```bash
mise run regenerate
# or, without mise:
uv run --with "kubex-codegen @ git+https://github.com/kubex-py/kubex-codegen@$(cat .kubex-codegen-version)" \
    kubex-codegen regenerate --k8s-version 1.37 --package-dir .
uv lock
```

The **Regenerate** workflow does the same every Monday (or on demand) and opens a pull request when
the models change.

## Releasing

The package has its own version numbers. Bump `version` in `pyproject.toml`, update
`CHANGELOG.md`, merge, then push a `vX.Y.Z` tag on `main`: `publish.yaml` publishes it to PyPI.
Every pull request from this repository publishes a `.devN` build to TestPyPI.
