# Setup balena CLI Action

This action installs the balena CLI in your GitHub Actions workflow
for interactions with balenaCloud like pushing releases.

## Usage

```yaml
uses: balena-io-examples/setup-balena-action@main
with:
  # balena CLI version to install (example: `v18.1.9`)
  # Default: 'latest'
  cli-version: ''

  # balena CLI release channel to install (example: `my-feature-branch`)
  # Mutually exclusive with `cli-version`
  # Default: ''
  cli-channel: ''

  # balenaCloud API token to login automatically
  # Default: ''
  balena-token: ''

  # Skip using the tool cache and always re-download
  # Default: 'false'
  skip-cache: ''
```

## Examples

### Install latest release

```yaml
- name: Setup balena CLI
  uses: balena-io-examples/setup-balena-action@main
```

### Install specific release

```yaml
- name: Setup balena CLI
  uses: balena-io-examples/setup-balena-action@main
  with:
    cli-version: v18.1.9
```

### Install from a release channel

Every balena CLI pull request publishes a build to a release channel named after
its branch, and finished releases are published to the `stable` channel. This is
the same mechanism `balena update <channel>` uses to switch an existing install.

```yaml
- name: Setup balena CLI
  uses: balena-io-examples/setup-balena-action@main
  with:
    cli-channel: my-feature-branch
```

A branch channel contains unreviewed code, and its contents change as the pull
request gains commits. Use it to test an unreleased fix, not in a workflow that
holds a production `balena-token`.

### Login to balenaCloud

```yaml
- name: Setup balena CLI
  uses: balena-io-examples/setup-balena-action@main
  with:
    balena-token: "*****"
```

### Login to balenaCloud staging

```yaml
- name: Setup balena CLI
  uses: balena-io-examples/setup-balena-action@main
  env:
    BALENARC_BALENA_URL: balena-staging.com
  with:
    balena-token: "*****"
```

### Push release to balenaCloud

```yaml
jobs:
  push:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup balena CLI
      uses: balena-io-examples/setup-balena-action@main
      with:
        balena-token: "*****"
    - name: Push release
      run: balena push myorg/myfleet
```
