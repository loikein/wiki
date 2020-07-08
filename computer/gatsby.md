# Gatsby

References:

- [Quick Start | GatsbyJS](https://www.gatsbyjs.org/docs/quick-start/)

## Basics

### Installation

Create new site from template:

```bash
# create a new Gatsby site using the garden theme starter
$ gatsby new garden-source https://github.com/mathieudutour/gatsby-starter-digital-garden

$ cd garden-source

# install dependencies
$ npm install

# update dependencies
$ npm update
```

If this happens: `npm WARN {something} requires a peer of {other thing} but none is installed. You must install peer dependencies yourself`, do this: \([credit]()\)

```bash
$ npm install --save-dev "{other thing}"
```

### Building Site

Build site:

```bash
# Generate HTML files, etc.
$ gatsby build

# Start local server
$ gatsby serve
```

Start debugging server:

```bash
$ gatsby develop
```

## Use External Path for Public Files

File tree:

```text
.
├── garden
│   ├── subdir
│   ├── index
│   ├── index.html
│   ├── page-data
│   ├── static
│   ├── webpack.stats.json
│   └── ...
└── garden-source
    ├── LICENSE
    ├── README.md
    ├── content
    ├── gatsby-config.js
    ├── gatsby-node.js
    ├── node_modules
    ├── package-lock.json
    ├── package.json
    └── public
```

Code to achieve this: \(credits: [1](https://github.com/gatsbyjs/gatsby/issues/14703#issuecomment-501916998), [2](https://github.com/gatsbyjs/gatsby/issues/18975#issuecomment-591403950), [3](https://github.com/gatsbyjs/gatsby/issues/18975#issuecomment-607329178)\)

```js
// In gatsby-node.js

// Copy public path elsewhere
// Use copy instead of move since `gatsby serve` only knows source/public
const path = require("path")
const fs = require("fs-extra")

exports.onPostBuild = function() {
    fs.copySync(path.join(__dirname, "public"), path.join(__dirname, "../garden"),{ overwrite: true })
}
```
