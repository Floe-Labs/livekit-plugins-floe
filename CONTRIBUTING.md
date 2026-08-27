# Contributing to livekit-plugins-floe

This is the Floe plugin for [LiveKit Agents](https://github.com/livekit/agents):
it routes LiveKit's `LLM` through [Floe](https://floefinance.com/) for metered,
budget-guarded inference, plus a usage reconciler and per-turn cost receipts.

The code is derived from the LiveKit Agents plugin layout and is licensed
Apache-2.0. The PyPI distribution is published as `livekit-plugins-floe-v1`
(dual-track with upstream), while the import namespace stays
`from livekit.plugins import floe`.

Contributions are welcome.

## Development setup

```bash
git clone https://github.com/Floe-Labs/livekit-plugins-floe.git
cd livekit-plugins-floe
pip install -e ".[dev]"
```

Run the checks before opening a PR:

```bash
pytest -q          # tests (test_floe.py)
ruff check .       # lint
ruff format .      # format
```

`pip install -e ".[dev]"` pulls the runtime deps (`livekit-agents[openai]`,
`floe-guard`, `livekit`, `aiohttp`) plus the test/lint tooling, so the suite
runs on a clean checkout.

## Contribution flow

1. Fork the repo and create a branch off `main` (e.g. `feat/your-change`).
2. Make your change with tests, and keep the checks above green.
3. Open a **draft pull request** against `main` and describe what changed and why.

## Code style

- Python 3.10+ with type hints (the package ships `py.typed`).
- Formatting and linting are handled by `ruff` (config in `pyproject.toml`) — run
  `ruff format .` and `ruff check .` before pushing.
- Leave the upstream LiveKit Apache-2.0 file headers intact.
- Prefer small, focused changes with tests that describe behavior.

## Releases

Publishing to PyPI is **not** automated on merge yet — the publish workflow is
`workflow_dispatch`-only and stays disabled until `PYPI_API_TOKEN` is added and
the PyPI project-name ownership is settled (see the README and FLO-748). Once
enabled, bump `version` in `livekit/plugins/floe/version.py` with the change.
