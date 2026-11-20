# Bloom Barista Academy

We recommend that you use the current [LTS version of Node JS](https://nodejs.org/en/download/package-manager) for this. At the time of writing, Node `v20.15.1` was used.

Once you've cloned the repository:
- Run `npm install`
- Run `npm start`

## NPM Scripts

| Script | Command | Description |
|---|---|---|
| `npm start` | `concurrently "eleventy --serve --quiet" "npm run css -- --watch"` | Starts the dev server with Eleventy live reload and PostCSS watch |
| `npm run build` | `npm run clean && eleventy && NODE_ENV=production npm run css` | Production build: cleans dist, runs Eleventy, compiles minified CSS |
| `npm run css` | `npx postcss src/css/*.css --dir dist/css` | Compiles CSS via PostCSS only |
| `npm run clean` | `rm -r -f dist && mkdir dist` | Removes and recreates the dist folder |
| `npm run patterns:create` | `node src/lib/code-sample-generator.js -b 'patterns'` | CLI generator for scaffolding new pattern stubs |

---

[Built with the CUBE CSS Boilerplate](https://piccalil.li/blog/a-css-project-boilerplate)
