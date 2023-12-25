---
title: "Pagefind"
---
[Pagefind](https://pagefind.app/) is a powerful searching extension for static sites that is fast, relatively easy to implement, and supports multilingual sites out of the box.

I am still trying it out over my blog, and maybe someday I will use it here too.

Doc pages to keep in mind:

- [Configuring what content is indexed | Pagefind — Static low-bandwidth search at scale](https://pagefind.app/docs/indexing/)

Example `netlify.toml` snippet:

```toml
[build]
publish = "public"
command = "hugo --gc --minify && npx -y pagefind@latest --site 'public'"

[context.production.environment]
NODE_VERSION = "18"
```
