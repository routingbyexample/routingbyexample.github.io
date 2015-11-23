# Routing By Example

This repository contains the source of [http://routingbyexample.com](http://routingbyexample.com).


## Sample content

When creating routing examples it can be difficult to come up with sample content for pages.

There is sample content available in the `export/sample-content` folder:

- **homepage**: `export/sample-content/homepage/homepage.html`
- **about**: `export/sample-content/homepage/about.html`

To use sample content in an example, simply make a component with a `templateUrl`:

```javascript
@Component({
  selector: 'about',
  templateUrl: 'http://routingbyexample.com/export/sample-content/about/about.html'
})
export class AboutCmp {
}
```

## Development

### Local development

First install the GitHub pages settings:

```bash
$ bundle install
```

To start a local development server:

```bash
$ bundle exec jekyll serve
```

To update the GitHub Pages settings

```bash
$ bundle update
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
