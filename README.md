# python-template

[Copier](https://copier.readthedocs.io) template for Python projects managed with [uv](https://docs.astral.sh/uv/).

Generated projects include:

- `src/` layout built with `uv_build`
- ruff for linting and formatting, pytest with coverage, hypothesis and xdist
- pre-commit hooks: file checks, gitleaks, ruff, lockfile check and conventional commit messages
- GitHub Actions: CI on pull requests (lint, commit messages, secret scan, tests) and automatic releases on merge to `main` with commitizen
- Dependabot for GitHub Actions and uv
- Optional `notebooks/` folder with output stripping

## Create a project

```bash
uvx copier copy gh:mvaldezc/python-template my-project
cd my-project
git init -b main
uv sync
uv run pre-commit install
git add -A && git commit -m "feat: initial project structure"
```

Then follow the *Repository setup* section in the generated README to configure the GitHub repository.

## Update a project

From the generated project, with a clean working tree:

```bash
uvx copier update
```

Copier compares the project with the template version it was generated from and applies the changes, merging them with local edits. Template versions are git tags on this repository, so tag a release after changing the template:

```bash
git tag 0.2.0 && git push origin 0.2.0
```

## Develop the template

Files under `template/` ending in `.jinja` are rendered with the answers from `copier.yml`. Other files are copied as they are, which is why the workflows have no `.jinja` suffix: their `${{ }}` expressions must not be rendered.

To try changes locally:

```bash
uvx copier copy --vcs-ref HEAD . /tmp/test-project
```
