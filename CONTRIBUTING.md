## Contribution Guidelines
We welcome feedback, bug reports, and pull requests!
For pull requests (PRs), please stick to the following guidelines:
* Before submitting a PR, verify that [an issue](https://github.com/luno/REPONAME/issues) exists that describes the bug fix or feature you want to contribute. If there's no issue yet, please [create one](https://github.com/luno/REPONAME/issues/new/choose).
* Fork REPONAME on your GitHub user account, make code changes there, and then create a PR against the main REPONAME repository.
* Add tests for any new features or bug fixes. Ideally, each PR increases the test coverage. We have a quality gate that checks.
* Follow the existing code style (follow [Effective Go](https://go.dev/doc/effective_go) where no obvious convention exists).
* Use the pull request template provided, and fill in all the details you can.
* Document newly introduced methods and classes with godoc-style comments, and add inline comments to code that is not self-documenting.
* Separate unrelated changes into multiple PRs.
* Commit messages should follow the conventions outlined at https://www.conventionalcommits.org/.
#### Hooks
Install pre-commit hooks before committing anything. After installing pre-commit (see [here](https://pre-commit.com/#install) for instructions), you can do this with:
```shell
pre-commit install --hook-type pre-commit --hook-type pre-push
```
Commits that have not run through pre-commit will be rejected, so please don’t skip them!
### Creating the PR
#### PR Title
Please follow the [Conventional Commits](https://www.conventionalcommits.org/) guidelines for PR titles (and commit titles)
#### PR Description
Please split the PR description into the categories defined by https://keepachangelog.com, for example:
```
### Added
- v1.1 Brazilian Portuguese translation.
### Changed
- Use frontmatter title & description in each language version template
```
If you are looking for help, or aren’t sure if something is an issue or not, please create a post under Discussions instead.
### Writing Tests

Where possible, we try to write unit tests in a [table-driven](https://go.dev/wiki/TableDrivenTests) way (something you’ll likely be familiar with if you’re familiar with Go). This doesn’t mean a test _has_ to be written in this way but if you find yourself in a situation where you are testing various inputs to a function that lead to different outputs, a table-driven test will work well!

Lastly, **don’t let review comments discourage you**! We appreciate any and all public contributions. Luno has an internal set of standards and guidelines we are committed to upholding on all of our repos, so we may request changes to bring any PRs in line with those.
