# Documentation Templates

This folder contains templates used to generate the project's `README.md` file using [gomplate](https://docs.gomplate.ca/).

## Files

- **`README.md.tmpl`** - The main template that generates the root `README.md`
- **`action.md.tmpl`** - A partial template that documents the action's inputs/outputs

## How It Works

The templates use the `action.yaml` file as a data source to automatically generate documentation. This ensures the README stays in sync with the action's actual inputs, outputs, and metadata.

## Generating the README

To regenerate the `README.md` file, run:

```bash
mise run docs
```

This will process the templates and output the result to `README.md` in the project root.

## Modifying Documentation

- **DO NOT** edit the root `README.md` directly - your changes will be overwritten
- Instead, edit the templates in this folder and regenerate the docs
