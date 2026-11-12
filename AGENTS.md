# General Agent Guidelines

This file provides guidance to code agents when working with code in this repository.

## Project Overview

This project is a playground for experimenting with Bayesian statistics.

## Development Commands

### Code Quality

```bash
uv run ruff check --fix && uv run ruff format        # Python linting/formatting
uv run ty check src tests                            # Python type checking
uv run pytest --no-cov -m "not integration" --quiet  # Python tests
```

## Coding Standards

* Avoid using `type: ignore`, `noqa`, and other code that disables calls to
  linters/checkers wherever possible.
* In general, functions, classes, etc. should be defined proceed in order from
  higher-level abstractions to lower-level abstractions. Avoid generating code that
  puts lower-level functions first, unless they must be defined first
  (ex: context managers).
* When generating Python function calls that must be wrapped over multiple lines, always
  place each parameter on its own line. The final parameter should be followed with
  a trailing comma, so that Ruff will enforce this.
* When raising exceptions, do not create an unnecessary `msg` variable and pass it
  to the constructor. Just pass the message to the constructor as a literal.
* When using the `typing` library, import the whole module with an alias of `T`, rather
  than importing needed types from the module.
* In general, favor importing packages (with a a short alias when sensible) rather than
  importing names from packages. For example: ```import numpy as np``` is preferred
  over ```from numpy import zeros```. Exceptions to this include `pathlib.Path` and
  imports within `__init__.py` files.
* Here are some preferred module import aliases:
  * dataclasses => dc
  * pytorch => pt
* Use comments instead of docstrings for classes/functions. This is not a reusable
  library, and it will not have generated documentation, so docstrings don't make any
  sense. But don't write class/function-level comments that just explain the obvious,
  only include them to avoid confusion. One exception here is for docstrings in
  Pydantic models, which are included in the schema.
