## Development

### Local development

To start a local development server:

```bash
$ jekyll serve
```

### Livereload

First install browser-sync:

```bash
$ npm install -g browser-sync
```

then start it and watch files in `_site`:

```bash
$ browser-sync start --proxy="localhost:4000" --files="_site/**/*"
```