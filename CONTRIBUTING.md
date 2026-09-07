# Contributing to DI-PASSIONATE

Thanks for your interest in our tools. This file applies to every repository in the
[DI-PASSIONATE](https://github.com/DI-PASSIONATE) organisation, unless a repository
ships its own `CONTRIBUTING.md`, which then takes precedence.

We are a small research team building EDA tooling in public. Outside contributions are
genuinely welcome, and a short conversation before you write code will save you time.

## Ways to contribute

- **Report a bug.** Open an issue in the repository concerned.
- **Suggest a feature.** Open an issue describing the design problem you are trying to
  solve, not only the feature you have in mind — the underlying use case often changes
  the answer.
- **Improve the documentation.** Corrections, clarifications and worked examples are as
  valuable as code, and are the easiest place to start.
- **Send a pull request.** See below.

Do **not** open a public issue for a security vulnerability — see
[SECURITY.md](SECURITY.md).

## Reporting a bug

A report we can reproduce is worth ten we cannot. Please include:

- what you did, what you expected, and what happened instead;
- the exact command or script, and the configuration file or netlist if one is involved
  (redact anything proprietary — a PDK path is enough, we do not need the PDK);
- the version of the tool, your Python version and your operating system;
- the versions of the external simulators involved (`Xyce --version`, `palace --version`,
  `gmsh --version`), since a surprising number of issues live there;
- the full error output, ideally with the verbose flag the tool offers (for COBRA:
  `cobra run config.json -v`, or `--log-file run.log` for a full debug log).

For COBRA, the output of `cobra doctor` tells us most of what we need about your
environment.

## Before you write code

Open an issue first for anything beyond an obvious fix, and say that you intend to work
on it. This avoids duplicated effort and lets us flag design constraints early — much of
this code sits on a shared pipeline, and a change that looks local often is not.

Small, self-evident fixes (a typo, a broken link, an off-by-one) need no discussion. Just
send the pull request.

## Development setup

All three repositories are Python projects targeting **Python 3.11+**. Check the
repository's README for anything specific; the common setup uses
[uv](https://docs.astral.sh/uv/):

```bash
git clone https://github.com/DI-PASSIONATE/<repository>.git
cd <repository>
uv sync                       # creates .venv/ from the lock file
uv run pytest                 # run the test suite
```

If you prefer another environment manager that is fine, but do not commit changes to the
lock file unless you deliberately changed a dependency.

Some functionality needs external tools that are not Python packages — Xyce, AWS Palace,
gmsh, Qucs-S. Tests that require them should skip cleanly when they are missing; if you
add one that does not, mark it so the suite stays runnable for everyone.

## Coding conventions

- **Match the surrounding code.** Consistency with the file you are editing beats
  personal preference.
- **Lint and type-check what you touched.** Where the repository configures them:
  ```bash
  uv run ruff check path/to/file.py
  uv run ty check path/to/file.py
  ```
  Fix the findings that concern your change; leave unrelated ones alone.
- **Type hints on new public functions**, and clear names over short ones.
- **Keep changes surgical.** Every changed line should trace back to the issue you are
  fixing. Do not reformat, rename or "improve" adjacent code in the same pull request —
  send that separately, and it will be reviewed on its own merits.
- **Validate inputs at boundaries** with actionable error messages. A user who mistypes a
  configuration key should be told which key, in which file.

## Tests

- Bug fixes come with a regression test that fails before the fix and passes after it.
- New behaviour comes with tests for the valid *and* the invalid case — configuration
  errors, missing files and bad paths are as much a part of the contract as the happy
  path.
- Tests must be hermetic: no absolute paths into a developer's home directory, no
  dependency on a PDK, no network access. Use the repository's fixtures and `tmp_path`.
- The full suite must pass before you open the pull request, and CI must be green before
  we merge.

## Documentation

If your change alters behaviour, configuration, CLI commands, outputs or workflows,
update the closest relevant documentation page in the same pull request. Prefer a short
example that matches the current code over prose. Keep the README, the docs and the
implementation consistent — and if you notice they already disagree, say so in the issue.

## Pull requests

- Branch off `main` and keep one logical change per pull request.
- Write a title that says what changed, and a description that says *why*, linking the
  issue it closes (`Closes #123`).
- Note anything a reviewer cannot see from the diff: a design trade-off you weighed, a
  case you deliberately did not handle, a manual test you ran against real hardware or a
  real PDK.
- Draft pull requests are welcome if you want feedback on a direction before polishing.

Reviews are done by a small team alongside research work, so please allow some time. A
polite ping on the pull request after a week or so is entirely reasonable.

## Licensing and attribution

Unless the repository states otherwise, our code is released under the
[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). By contributing you
agree that your contribution is licensed under the same terms, and that you have the
right to submit it — if your employer or institution holds rights to your work, make sure
you are cleared to contribute before you do.

If you use these tools in academic work, please cite them; each repository's
`CITATION.cff` has the current reference.

## Code of conduct

Be respectful, assume good faith, and keep discussion technical. We are an academic
project and expect the standards of a professional research environment: critique ideas
and code, not people. Behaviour that makes others unwelcome — harassment, personal
attacks, discriminatory language — is not tolerated, and maintainers may edit, lock or
remove contributions that violate this. Concerns can be raised privately with the
maintainers of the repository concerned.
