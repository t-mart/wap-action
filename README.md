# t-mart/wap-action

Build and optionally publish your WoW addon package with [wap](https://github.com/t-mart/wap).

## Example

```yaml
jobs:
  build-and-release:
    name: Check
    runs-on: 'ubuntu-latest'
    steps:
      # do other steps, and then...
      - name: 'wap'
        uses: 't-mart/wap-action@master'
        with:
          - release-type: 'release'
          - curseforge-token: '${{ secrets.CURSEFORGE_TOKEN }}'
```

## Inputs

- `release-type`

  **Type**: any of `none`, `alpha`, `beta`, or `release`

  **Default**: `alpha`

  If set to `alpha`, `beta`, or `release`, run
  [`wap publish`](https://t-mart.github.io/wap/commands/publish/) after building.

  If set to `none`, do not publish.

  ```yaml
  - name: wap
    uses: t-mart/wap-action@v1
    with:
      - release-type: 'none'
  ```

- `curseforge-token`

  **type**: string

  **Default**: `token-not-set`

  The token to use for publishing. This input is unused if `release-type == 'none'`.

- `config-path`

  **type**: string

  **Default**: `./wap.json`

  The path of the configuration file used to run the wap commands.

  ```yaml
  - name: wap
    uses: t-mart/wap-action@v1
    with:
      - config-path: './custom-wap.json'
  ```

## How it works

This is a composite action that:

- sets up the latest 3.12.x Python
- pipx installs wap (with that new Python)
- `wap build` ...
- optionally, `wap publish`
