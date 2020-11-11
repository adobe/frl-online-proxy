The docs are built manually because this theme does not work well with Github Pages' Jekyll environment.

For maximum ease of use, this branch should be checked out to its own special directory.

```
$ git clone https://github.com/adobe/frl-online-proxy.git frl-online-proxy-docs
$ cd frl-online-proxy-docs && git checkout gh-pages
```

The build process is pretty simple:

1. `cd frl-online-proxy-docs/src`
2. `bundle exec jekyll build -d ../docs`
3. `cd .. && git add . && git commit -m "update docs" && git push`
