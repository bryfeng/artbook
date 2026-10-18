# artbook.dev

The landing page for [artbook.dev](https://artbook.dev), home of [Artspo](https://github.com/bryfeng/artspo).

One static page, no build step. GitHub Pages serves this branch at the custom domain in `CNAME`.

## The library

`library/` is an Artspo book: the page at [artbook.dev/library](https://artbook.dev/library/), `artbook.md`, and the
agent catalogue (`llms.txt`, `agents/menu.json`, one JSON per pattern and clip). It is generated; don't edit it by
hand. Rebuild it from a library with:

```sh
python3 ~/code/artspo/extension/skills/artspo/catalogue.py ~/Downloads/artspo --public --no-works \
  --site library --title "The Artbook library" --url https://artbook.dev/library/ \
  --description "Design languages, techniques and measured websites for coding agents to shop. Every item is a standalone prompt. Made with Artspo."
```

`llms.txt` at the root is hand-written and points agents at the library.
