# Stencil Subcategories Example Lab Project

This is an example developer project demonstrating how to customize a Stencil codebase. 

## Lab Steps and Commit History

The commit history of the repository is important and represents the steps of the developer labs. Each commit starting with the `start` tag demonstrates the code changes in a lab step.

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
