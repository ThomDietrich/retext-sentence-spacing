# retext-sentence-spacing [![Build Status][travis-badge]][travis] [![Coverage Status][codecov-badge]][codecov]

Check spacing (one or two spaces) between sentences with
[**retext**][retext].

## Installation

[npm][npm-install]:

```bash
npm install retext-sentence-spacing
```

## Usage

Say we have the following file, `example.txt`:

```text
One sentence. Two sentences.

One sentence.  Two sentences.
```

And our script, `example.js`, looks as follows:

```javascript
var vfile = require('to-vfile');
var report = require('vfile-reporter');
var retext = require('retext');
var spacing = require('retext-sentence-spacing');

retext()
  .use(spacing)
  .process(vfile.readSync('example.txt'), function (err, file) {
    console.error(report(err || file));
  });
```

Yields:

```text
example.txt
  3:14-3:16  warning  Expected `1` space between sentences, not `2`  retext-sentence-spacing  retext-sentence-spacing

⚠ 1 warning
```

This plugin can be configured to prefer 2 spaces instead:

```diff
 retext()
-  .use(spacing)
+  .use(spacing, {preferred: 2})
   .process(vfile.readSync('example.txt'), function (err, file) {
```

Yields:

```text
example.txt
  1:14-1:15  warning  Expected `2` spaces between sentences, not `1`  retext-sentence-spacing  retext-sentence-spacing

⚠ 1 warning
```

## API

### `retext().use(sentenceSpacing[, options])`

Emit warnings when the spacing between two sentences does not adhere
to the preferred style.

###### `options.preferred`

`1` or `2`, default: `1` — Number of expected spaces.

## Related

*   [`retext-contractions`](https://github.com/wooorm/retext-contractions)
    — Check apostrophe use in contractions
*   [`retext-diacritics`](https://github.com/wooorm/retext-diacritics)
    — Check for proper use of diacritics
*   [`retext-quotes`](https://github.com/wooorm/retext-quotes)
    — Check quote and apostrophe usage

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definitions -->

[travis-badge]: https://img.shields.io/travis/wooorm/retext-sentence-spacing.svg

[travis]: https://travis-ci.org/wooorm/retext-sentence-spacing

[codecov-badge]: https://img.shields.io/codecov/c/github/wooorm/retext-sentence-spacing.svg

[codecov]: https://codecov.io/github/wooorm/retext-sentence-spacing

[npm-install]: https://docs.npmjs.com/cli/install

[license]: LICENSE

[author]: http://wooorm.com

[retext]: https://github.com/wooorm/retext-sentence-spacing
