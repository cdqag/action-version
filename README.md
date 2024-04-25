# Action Version

Action that does the versioning according to [Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/) and [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## Prerequisites

Environment Variables:

* `BRANCH_NAME` - current branch name; either use [cdqag/action-init](https://github.com/cdqag/action-init) or set it manually

## Usage

```yaml
# You need init, otherwise you will need to set env BRANCH_NAME on your own
- uses: cdqag/action-init@master
- uses: cdqag/action-version@master
```

### Inputs

| Name     | Description                                            | Default    |
|----------|--------------------------------------------------------|------------|
| `pep440` | Use PEP440 format? (`1.2.3+dev` instead `1.2.3-dev`)   | `false`    |

### Outputs

* `current-version` - current detected version
* `new-version` - new calculated version
* `new-major-version` - new calculated major version

#### Environment Variables

* `CURRENT_VERSION` - current detected version
* `NEW_VERSION` - new calculated version
* `NEW_MAJOR_VERSION` - new calculated major version

## How it Works

### SemVer Briefly

* SemVer defines the version syntax following way: **MAJOR.MINOR.PATCH**
* **MAJOR** should be increased if any breaking change has been introduced
* **MINOR** should be increased if any backward compatible feature
* **PATCH** should be increased if any backward compatible fix has been introduced

### Conventional Commits Briefly

* CC defines the commit message syntax following way:

`<type>[optional scope]: <description>`

Examples:

* `BREAKING CHANGE: Change the interface of XYZ endpoint` | **MAJOR** change
* `feat!: Change the interface of XYZ endpoint` | **MAJOR** change
* `feat: Add new XYZ endpoint` | **MINOR** change
* `fix(CDLD-XYZ): Use newer version of Gradle ABC plugin` | **PATCH** change

### Examples

#### Example 1

* `currentVersion` is `1.0.0`
* `releaseBranch` is `master` (you don't need to set it, because it's the default value)
* `currentBranch` is `master`
* Last commit messages are:

  * `fix: One`
  * `feat: Two`
  * `chore: Three`

* `newVersion` will be `1.1.0`

#### Example 2

* `currentVersion` is `1.2.3`
* `releaseBranch` is `some-task` (you don't need to set it, because it's the default value)
* `currentBranch` is `master`
* Last commit messages are:

  * `fix: One`
  * `feat!: Two`

* `newVersion` will be `2.0.0-some-task`

#### Example 3

* `currentVersion` is `1.2.3`
* `releaseBranch` is `some-task` (you don't need to set it, because it's the default value)
* `currentBranch` is `master`
* `strict` is `true`
* Last commit messages are:

  * `fix: One`
  * `feat!: Two`
  * `yolo commit`

* Plugin will throw an Exception, because strict mode is enabled, and `yolo commit` is not CC-valid
