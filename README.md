# GitHub workflows for usage with ReSpec repositories.

A [cookiecutter](cookiecutter.readthedocs.io) template for workflows in a repository that hosts (CROW-style) documents.
The [stichting-crow/respec-repo-template] uses this template for a new repository.

> **Wat betekent dit voor mij**:
>
> - Voor een nieuw project: volg het stappenplan op [stichting-crow/respec-repo-template].
> - Om deze workflows toe te voegen aan een bestaand project:
>   - Controleer of de Git-instellingen van je project overeenkomen met het hieronder gespecificeerde.
>   - Voer daarna onderstaande CLI-commando uit.

## Usage

There is no need to clone this repository.
Run the below commands from the command line (requires `python` and `pip`).

```cli
$ cd .github/  # from the repo root.
$ pip install cookiecutter
$ cookiecutter gh:stichting-crow/respec-workflows-template
```

## Architecture

The workflows expect the following:

- branch `main` is used for editing.
- directory `docs/` is used as the deploy base, i.e., ReSpec-documents are subdirs in `docs/`.
- branch `gh-pages` is used for GitHub Pages deployment.
- no dir `docs/` in `gh-pages`, but there is one for reference versions (`v/`).
- The `gh-pages` branch is protected.
- In GitHub Pages settings: serve from branch `gh-pages`, folder `/`.

If you want to use this template, ensure the above conditions before installing the workflows.

## Workflows

| file                                     | triggers                                       | desc                                                                     |
| ---------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------ |
| [`add-doc.yaml`](add-doc.yaml)           | workflow_dispatch                              | on request, add a document to `main:docs/`                               |
| [`auto-publish.yaml`](auto-publish.yaml) | push (`main`), workflow_dispatch, workflow_run | on push to `main`, autopublish to GitHub Pages                           |
| [`lifecycle.yaml`](lifecycle.yaml)       | workflow_dispatch                              | on request, add `v/...` to `gh-pages:/`                                  |
| [`deploy.yaml`](deploy.yaml)             | workflow_run \*                                | trigger redeploy, report on what documents are served from `gh-pages:` . |

[stichting-crow/respec-repo-template]: https://github.com/stichting-crow/respec-repo-template
[respec-repo-template-generate]: https://github.com/stichting-crow/respec-repo-template/generate
