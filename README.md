# Python Modules

Exercises from the 42 Python curriculum, organized as independent Git
repositories and linked here as submodules.

## Modules

- `python-module-01`: object-oriented garden systems
- `python-module-02`: exceptions and defensive programming
- `python-module-03`: Python collections and generators
- `python-module-04`: files, streams, and context managers
- `python-module-05-bis`: environments, dependencies, and packages
- `python-module-06-bis`: abstract architectures and design patterns

## Clone

```sh
git clone --recurse-submodules \
  https://github.com/viniciusnevescosta/Python-Modules.git
```

For an existing clone:

```sh
git submodule update --init --recursive
```

## Environment

The exercises target Python 3.10 or newer and were validated with Python
3.14.8, `flake8`, and `mypy --strict`.

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install flake8 mypy
```

Module 05 declares its additional dependencies in its own requirements files.
