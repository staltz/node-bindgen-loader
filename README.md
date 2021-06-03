# node-bindgen-loader

> Bindings loader for [node-bindgen](https://github.com/infinyon/node-bindgen) that supports prebuilds.

```
npm install node-bindgen-loader
```

Based on [neon-load-or-build](https://github.com/staltz/neon-load-or-build) except it does **not** conditionally compile your node-bindgen module.

## Usage

In your node-bindgen module's `index.js`, instead of using the default `require('./dist/index.node')`, use `node-bindgen` to load your binding.

```js
module.exports = require('node-bindgen-loader')({
  moduleName: 'my-package', // optional but recommended
  dir: __dirname,
})
```

**When targeting nodejs-mobile, you must have `moduleName`**, because it more accurately finds the correct path on both iOS and Android, even if you use `noderify` (or even if you don't).

Prebuilds will be attempted loaded from `MODULE_PATH/prebuilds/` and then next `EXEC_PATH/prebuilds/`.

## Supported prebuild names

If so desired you can bundle more specific flavors, for example `musl` builds to support Alpine, or targeting a numbered ARM architecture version.

These prebuilds can be bundled in addition to generic prebuilds; `node-bindgen-loader` will try to find the most specific flavor first. Prebuild filenames are composed of _tags_. The runtime tag takes precedence, as does an `abi` tag over `napi`. For more details on tags, please see [`prebuildify`][prebuildify].

Values for the `libc` and `armv` tags are auto-detected but can be overridden through the `LIBC` and `ARM_VERSION` environment variables, respectively.

## License

MIT
