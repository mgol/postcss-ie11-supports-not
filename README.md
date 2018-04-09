# `postcss-ie11-supports` [![Build Status][ci-img]][ci]

[PostCSS] plugin adding `@supports not` support for IE 11.

[PostCSS]: https://github.com/postcss/postcss
[ci-img]:  https://travis-ci.org/mgol/postcss-ie11-supports.svg
[ci]:      https://travis-ci.org/mgol/postcss-ie11-supports

This plugin adds basic support for `@supports` in IE 11. It makes IE skip all `@supports` block but apply all `@supports not` ones. Since `@supports` is generally used for APIs newer than IE 11 this is an acceptable solution.

The way it does this is by prepending a selector understood by IE 11 only to the existing selector, making all other browsers ignore this rule.

Example input:
```css
@supports (display: grid) {
    .box { /* Grid styles */ }
}
@supports not (display: grid) {
    .box { /* Fallback styles */ }
}
```

Example output:
```css
@supports (display: grid) {
    .box { /* Grid styles */ }
}
@supports not (display: grid) {
    .box { /* Fallback styles */ }
}
:-ms-fullscreen, .box { /* Fallback styles */ }
```

## Usage

```js
postcss([
    require('postcss-ie11-supports'),
])
```

### Options

`ieSelector`: A selector used to taint a block cloned outside of `@supports not` so that it's accepted in IE 11 only. By default `':-ms-fullscreen'`, can be changed to e.g. `:-ms-lang(x)` to support IE 10 as well. Use with caution so that good browsers are not punished!

See [PostCSS] docs for examples for your environment.
