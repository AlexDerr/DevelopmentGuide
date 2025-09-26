# Git CI

Documentation: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Steps to include:
- Install dependencies
- Sort imports
- Formatting
- Linting
- Unit tests
- Test Docker builds

## Examples

Python example in MLTE: https://github.com/mlte-team/mlte/blob/master/.github/workflows/ci.yaml

```yaml
# ~/.github/workflows/ci.yaml

# Name of the CI
name: Example CI

# When to trigger the CI
on:
  - push
  - pull_request

# List of jobs to run
jobs:
  first-job:
    # Creates matrix strategy for jobs to create several jobs with variable combinations
    strategy:
      matrix:
        os: [ubuntu-latest]
        language-version: ['3.11', '3.12']
    # Define platform to run the tests on
    runs-on: ${{ matrix.os }}
    # All of the actions to take as part of this job
    steps:
      # Use a reusable workflow file as a step, this action checks out the repo
      #   https://github.com/actions/checkout
      - uses: actions/checkout@v4
      # Set up a language if needed for tests to run, for eample python
      #   https://github.com/actions?q=setup&type=all&language=&sort=
      - name: Set up language ${{ matrix.language-version }}
        uses: actions/setup-python@v5
        with:
          language-version: ${{ matrix.language-version }}
      - name: First step
        run: first step command
      - name: second step
        run: second step command

  second-job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
```
