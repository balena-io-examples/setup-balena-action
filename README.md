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

  # balenaCloud API token to login automatically
  # Default: ''
  balena-token: ''
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
