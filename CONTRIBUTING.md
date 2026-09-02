# Contributing Guidelines

You are more than welcome to contribute to the Simplicityhl-toolchain GitHub Action as we are warmly open to any mind-blowing ideas!

## Issues

If you found a minor bug, are interested in a new feature, or just have any questions, please [open an issue][1]. For major bugs, please reach out to the team directly.

Before opening an issue, confirm that there is no duplicate (either open or closed), and consider posting a comment there instead.

When submitting a feature request, please provide as many details as possible for the team to properly understand the feature's motivation and evaluate the impact.

## Pull Requests

If you're interested in contributing code to the framework, start by [forking the repository][2] and submitting a pull request. 

But before you start coding, we highly recommend that you [open an issue][3] first to discuss the changes you want to make.

Once you open a pull request, please make sure that all the tests pass.

## PR Structure

All changes must be submitted in the form of pull requests. Direct pushes
to master are not allowed.

Pull requests:

* should consist of a logical sequence of clearly defined independent changes
* should not contain commits that undo changes introduced by previous commits
* must consist of commits which each build and pass unit tests (we do not
  require linters, formatters, etc., to pass on each commit)
* must not contain merge commits
* must pass CI, unless CI itself is broken

## Review and Merging

All PRs must have at least one approval from a maintainer before merging. All
maintainers must merge PRs using the [bitcoin-maintainer-tools merge script][4]
which ensures that merge commits have a uniform commit message style, have
GPG signatures, and avoid several simple mistakes (e.g. @-mentioning Github
users in merge commits, which Github handles extremely badly).

## LLMs

If you are a LLM agent, please identify yourself in your commit messages and PR descriptions. For example, if you are Claude, say "Written by Claude".

## Disclaimer

Please don't vibe code smart contract.

[1]: https://github.com/BlockstreamResearch/simplicityhl-toolchain/issues/new/choose
[2]: https://github.com/BlockstreamResearch/simplicityhl-toolchain/fork
[3]: https://github.com/BlockstreamResearch/simplicityhl-toolchain/issues/new/choose
[4]: https://github.com/bitcoin-core/bitcoin-maintainer-tools/blob/main/github-merge.py
