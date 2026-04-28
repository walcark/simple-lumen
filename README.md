# simple-lumen

A proof-of-concept for a simplified radiative transfer model backed by a Monte-Carlo sampler and a C++/CUDA kernel.

The goal is to explore a clean Python API that can be incrementally extended with new optical elements while remaining easily pluggable onto a low-level CUDA kernel.

## Simplified hypotheses

- The medium is homogeneous, non-absorbing, and isotropic.
- There are no 3D objects or surfaces within the medium.
- The only optical system is a Gaussian light source emitting toward a plane-parallel surface.
- The surface collects photons crossing it, with no notion of time spent in the medium.

## Open questions

- What is the simplest kernel design that remains pluggable on a Python-defined medium / 3D scene? More specifically, how should the Python API be structured so that new optical elements can be added without rewriting the C++ side?
- Can this system be coupled with [Torch Lens Maker](https://github.com/victorpoughon/torchlensmaker)?

## Requirements

- [Pixi](https://pixi.sh) — manages the Conda/PyPI environment.
- CUDA 12.6 — required for the GPU environment.

## Installation

```bash
git clone <repo-url>
cd simple-lumen
pixi install
```

## Development

All tasks run through Pixi:

```bash
pixi run -e test fmt        # auto-format with ruff
pixi run -e test lint       # lint with ruff
pixi run -e test typecheck  # type-check with mypy
pixi run -e test test       # run the test suite
pixi run -e test all        # run all of the above
```

Tests that depend on a CUDA device are automatically skipped when no GPU is available.
