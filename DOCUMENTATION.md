# Documentation

## About

The documentation roughly attempts to follow [Diátaxis](https://diataxis.fr/).

Prose conventions: [docs/STYLE.md](./docs/STYLE.md).

## View

You can [view the moccasin documentation here](https://cyfrin.github.io/moccasin/).

## Build

To build the documentation:

1. Follow the `Installing for local development` instructions in [CONTRIBUTING.md](./CONTRIBUTING.md).

2. Add dependencies:

```bash
uv sync --all-extras
```

3. Build the documentation:

```bash
just docs
```

4. Open the documentation in your browser.

If using something like VSCode's live server:

```text
http://127.0.0.1:5500/built_docs/html/index.html
```

Or open `built_docs/html/index.html` directly from your filesystem.

## Edit workflow

- Style guide: [docs/STYLE.md](./docs/STYLE.md)
- Live rebuild while editing RST: `just docs-watch`
