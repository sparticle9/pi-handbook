# Contributing

This handbook is a community project. No contribution is too small.

## What we're looking for

- Typo fixes, grammar improvements, broken links
- Better code examples or updated snippets
- New sections, tips, or workflow patterns you've discovered
- Extensions or skills you've built — write them up, share the code
- Corrections to anything that's wrong or outdated
- Screenshots, terminal recordings, or diagrams
- Translations

The [Limitations](09-limitations.md) page documents known gaps. Building solutions for those and writing them up here is the highest-impact work you can do.

## How to contribute

1. Fork [sparticle9/pi-handbook](https://github.com/sparticle9/pi-handbook)
2. Edit or add markdown files in `docs/`
3. Open a PR with a short description of what you changed and why

That's it. No build step required — the site deploys automatically on merge.

## Guidelines

- Write in plain, direct English. No fluff, no hype.
- Be honest about limitations. Don't oversell pi or undersell alternatives.
- All quotes must be attributed with source links.
- Keep code snippets runnable and minimal.
- Use MkDocs Material admonitions for callouts:

    ```markdown
    !!! tip
        This is a tip.

    !!! warning
        This is a warning.
    ```

- New chapters go in `docs/` and must be added to `nav:` in `mkdocs.yml`.
- When comparing tools, be fair. State facts, cite sources.

## Local preview

```bash
pip install mkdocs-material
mkdocs serve
# http://localhost:8000
```

## What not to do

- Don't add vendor-specific promotional content
- Don't commit credentials or API keys
- Don't use AI-generated filler text
- Don't remove the disclaimer about unofficial status

## License

Content is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). By contributing, you agree to license your work under the same terms.
