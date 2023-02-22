# Jekyll

References:

- [Quickstart | Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/)

## Basics

### Installation

### Start new site

```bash
# In parent folder

$ jekyll new a-website
$ cd a-website
```

Fixes:

- In `.gitignore` add: `Gemfile.lock`
- In `Gemfile` add: `gem "webrick"`


Update or install gems:

```bash
# If `Gemfile.lock` does not exist
$ bundle install

# Otherwise
$ bundle update
```


Start local server: (the address is `Server address`)

```bash
$ bundle exec jekyll serve --livereload

# In the case of GitHub Pages
$ bundle exec jekyll serve --livereload --safe
```
