# ghtags

Generate releases/changelog/history file from tags(default)/releases
of a GitHub repo.

The output file is written in markdown and commit messages are used for tags.

> The [CHANGELOG.md](assets/CHANGELOG.md) in this repo is generated by using `ghtags`
> from the [releases](https://github.com/r0mflip/ghtags/releases/).


## Installation

``` sh
$ npm i -g ghtags
```

## Usage

``` sh
$ ghtags --repo expressjs/express \
    --token <GitHubAccesToken> \       # Personal access token for GitHub API
    --out <OutputFile>.md \            # Output to file, default is stdout
    --releases                         # Use GitHub releases for data
```

### Options
- `--repo <repo>` Specify repo in `<scope>/<repo>` format (`-r`)
- `--token <token>` - GitHub access token (`-t`)
- `--out <file>` - Save formatted markdown output into file (`-o`)
- `--releases` - If specified gets info from releases [uses tags by default]
- `--noempty` - Skip entities with empty or same body as release name (`-n`)

_**Note:**_ Equivalent of `--noempty` and `--out` are not available programatically

## API

```js
const getTags = require('ghtags');

// getTags is an AsyncGeneratorFunction
// which returns an AsyncGenerator
const tagSpitter = getTags({
  repo: 'expressjs/express',
  token: '<GITHUB_TOKEN>',
  releases: false,
});

(async _ => {
  for await (const tag of tagSpitter) {
    // Use tag of type
    AsyncGenerator<{
      url: String;
      name: String;
      author: String;
      prerelease: Boolean;
      date: String;
      body: String;
    }, void, unknown>
  }
})();
```

Know more about [Asynchronous generators](https://exploringjs.com/impatient-js/ch_async-iteration.html#async-generators)

# LICENSE
[MIT](LICENSE)
