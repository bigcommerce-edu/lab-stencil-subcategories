# Stencil Subcategories Example Lab Project

This is an example developer project demonstrating how to customize a Stencil (Cornerstone) codebase by adding a subcategory listing to the category page.

## Terminology and Git Model

This repository maintains two kinds of history **separately**:

- **Traditional branch** (`main`): a normal Git branch with stable, append-only history. Custom-code changes are made on feature branches, reviewed via pull request, and merged here. `main`'s history is never rewritten.
- **Progressive history**: a tutorial-shaped commit chain (clean framework install → step commits → end metadata) that represents the step-by-step lab progression. It is rebuilt as an independent commit chain and identified by a **project-version tag** (plain semver) at its tip plus the step tags along it.

`main` and the latest progressive history have **different tip commits but identical file trees**. Every change must be replicated across both, using the `bcedu-lab-sync` skill, and verified with its `validate-sync` command:

- **Framework/dependency upgrades**: rebuild a new progressive history with `bcedu-lab-upgrade`, then `sync-to-main` (a reviewed PR) brings it onto `main`.
- **Custom lab-code changes**: make them on a branch off `main` and merge via PR, then `sync-to-progressive` folds them into a rebuilt progressive history.
- **Publishing** a progressive history (moving step tags + creating the project-version tip tag) is done with `bcedu-lab-publish`; it does **not** advance `main`.

## Project Version and Changelogs

- The **project version** (plain semver, separate from the Cornerstone framework version) is held in `package.json`'s `version` field and tagged on the tip of the corresponding progressive history.
- Each version has a changelog entry in `changelogs/<version>.md`. (This is distinct from `CHANGELOG.md`, which is Cornerstone's upstream framework changelog.)
- **Metadata at the end**: the project-version bump and the addition of changelog entries and tutorial docs are folded into the final commit(s) of each rebuilt progressive history (amended on each rebuild rather than accumulating new commits).
- The lab steps and GitHub diff links live in `docs/TUTORIAL.md`, which carries a "Based on version X" banner matching the latest progressive history.

## Tag Conventions

- **Project-version tag**: plain semver (e.g. `1.0.0`) at a progressive history's tip. Created fresh per history; never migrated.
- **Framework anchor**: `framework-<semver>` (e.g. `framework-6.17.0`) marks a base-framework (Cornerstone) release point. Permanent; never migrated.
- **Step tags**: `<prefix>-NN-pre` / `<prefix>-NN-post`, plus `start` / `complete` for the overall lab. Migrated onto a new history by the Main Tags publish.
- **eLearning tags**: `e-` prefixed. Migrated by the eLearning publish.

## Commit History Structure

- The first commit is a clean Cornerstone install.
- **Strict 1:1 TODO → code**: each commit that introduces `TODO:` comments is immediately followed by the code commit that resolves them (one TODO commit per code commit). Avoid bundling many TODOs into a single early commit.

### Lab Exercises

| Exercise | Description | Tag Prefix |
| ------ | ----------- | ---------- |
| Main | Add Subcategories Listing | `lab` |

### Lab Step Breakdown

Each step is a `<tag>-pre` (TODO placeholders) commit immediately followed by a `<tag>-post` (implementation) commit. eLearning state is represented by the same base tags in `e-<tag>-pre`/`e-<tag>-post` format.

**Add Subcategories Listing (`lab`)** — start: `start`, complete: `complete`

| Step | Tag Base | Description |
| ---- | --- | ----------- |
| 1 | `lab-01` | Add subcategories placeholder to category page |
| 2 | `lab-02` | Add subcategory listing component |
| 3 | `lab-03` | Add subcategory listing styles |
| 4 | `lab-04` | Add theme config settings for styles |

> Note: the current history bundles the initial lab TODOs into a single early commit (`lab-01-pre`), which does not yet satisfy the strict 1:1 TODO → code rule. Restructuring those into per-step TODO/code pairs is a planned follow-up effort.

## File Removal - Protected Paths

When creating a clean orphan branch, the following additional file paths should be protected from removal:

* `config.stencil.json`
* `secrets.stencil.json`

## Framework Install Command

The base framework is the Cornerstone theme. Clone Cornerstone from GitHub:

```
git clone git@github.com:bigcommerce/cornerstone.git --branch <version>
```

After re-installing the framework, make sure an appropriate version of Node.js is installed according to `.nvmrc` and use `npm install` to install dependencies.
