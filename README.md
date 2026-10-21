# Silk Homebrew tap

Homebrew formulae for [Silk](https://github.com/silk-lang/silk).

```sh
brew install silk-lang/tap/silk
```

or `brew tap silk-lang/tap` once and then `brew install silk`.

Supported platforms are the ones Silk publishes compilers for: macOS on Apple Silicon, and Linux
on x86-64 and ARM64. The formula depends on Homebrew's `llvm` and points `silk` at its Clang;
set `SILK_CLANG` or pass `--clang` to use another one.

## Which release

`silk` follows the same channel as `install.sh`: the latest stable release, or the newest
published dev release while no stable release exists yet.

## How the formula is updated

[`scripts/update-formula.sh`](scripts/update-formula.sh) picks the release, downloads each target
archive, checks its minisign signature against the Silk release key and GitHub's digest, and
writes [`Formula/silk.rb`](Formula/silk.rb) with the archive SHA-256s pinned.

The [update workflow](.github/workflows/update.yml) runs it every two hours (or on demand, with an
optional exact tag), installs and tests the regenerated formula on macOS arm64 and Linux x86-64
(Linux arm64 is tested but not required), and commits it only when those pass. Pushes and pull
requests run the same install test against the formula as committed.

To update by hand:

```sh
scripts/update-formula.sh            # or: scripts/update-formula.sh v0.1.0-dev.5+1ff1cde7cde4
```

It needs `curl`, `jq`, `minisign` and `sha256sum`.
