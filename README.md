# Action Version

This composite GitHub Action calculates the new version using [Conventional Commits 1.0](https://www.conventionalcommits.org/en/v1.0.0/) and [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).
It uses under the hood [ietf-tools/semver-action@1](https://github.com/ietf-tools/semver-action/tree/v1/).

The important feature of this action is that it appends the suffix to the version, based on current branch.

* If the branch is the default one, it doesn't append anything. So e.g. `1.2.3`.
* Else it appends the short SHA of the commit. So e.g. `1.2.3-abcdef1`.
* Additionally you can set flag `pep440-compliant` to `true` to use PEP440 format. So e.g. `1.2.3+abcdef1`.

## Usage

```yaml
- name: Calculate new version
  id: version
  uses: cdqag/action-version@v2
```

### Inputs

| Name | Description | Default |
|---|---|---|
| `pep440-compliant` | Use PEP440 format? (`1.2.3+dev` instead `1.2.3-dev`) | `false` |

### Outputs

* `current-version` - current detected version
* `new-version` - new calculated version
* `new-major-version` - new calculated major version

#### Environment Variables

* `CURRENT_VERSION` - current detected version
* `NEW_VERSION` - new calculated version
* `NEW_MAJOR_VERSION` - new calculated major version

## License

This project is licensed under the Apache-2.0 License. See the [LICENSE](LICENSE) file for details.
