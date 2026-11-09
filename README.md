# brizz-python

Release notes for the [Brizz](https://brizz.ai) Python SDK, [`brizz`](https://pypi.org/project/brizz/) on PyPI.

The SDK traces your AI agent — every conversation, LLM call and tool call — and sends it to Brizz, the product analytics layer for AI agents.

This repo holds the changelog and a GitHub release per published version. The SDK source is not published here.

## Install

```bash
pip install brizz
```

## Quick start

```python
from brizz import Brizz

Brizz.initialize(api_key="<your Brizz API key>", app_name="my-agent")
```

Full setup: the [`brizz` README on PyPI](https://pypi.org/project/brizz/).

## Changelog

- [CHANGELOG.md](./CHANGELOG.md)
- [Releases](https://github.com/brizzai/brizz-python/releases)

## Reporting issues

https://github.com/brizzai/brizz-python/issues

## License

The contents of this repository are Apache-2.0 licensed; see [LICENSE](./LICENSE). The `brizz` package on PyPI is distributed under the license stated in its metadata.
