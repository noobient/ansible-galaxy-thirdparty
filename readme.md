# bviktor.thirdparty

## Synopsys

This role lets you install packages from third party repositories.

## Parameters

| Name | Required | Example | Description |
|---|---|---|---|
| `name` | yes | `Defender ATP` | Package nick name, only for informative purposes during the run. |
| `package` | yes | `mdatp` | Package name to be installed from the repo. |
| `version` | no | `101.73.77` | Package version to install. If specified, the package will also be locked to that version with `apt-mark hold` or `dnf versionlock`. |
| `repo_file` | no | `microsoft-prod` | Repo file in your `templates` directory without the `.repo.j2` or `list.j2` suffix. If not specified, you must specify `repo_url`. |
| `repo_url` | no | `https://packages.microsoft.com/config/rhel/8/prod.repo` | Repo file URL. If not specified, you must specify `repo_file`. |
| `gpg_url` | no | `https://packages.microsoft.com/keys/microsoft.asc` | URL for the GPG file used to sign the repo. |
| `gpg_file` | no | `nordlayer-keyring` | GPG file in your `files` directory without the `.asc` suffix. Not recommended, since GPG keys regularly change in most repos. |
| `gpg_server` | no | `keyserver.ubuntu.com` | GPG server address to import the key from. Only supported on Debian derivatives. |
| `gpg_id` | no | `ACCAF35C` | ID of the key hosted on the GPG server. Only supported on Debian derivatives. |
| `ldconfig` | no | `true` | If `true`, ldconfig is ran after the installation finishes. Useful when installing libraries that extend `LD_LIBRARY_PATH`. |
| `repo_overwrite` | no | `true` | If `true`, the repo file is deployed once more after package installation. Useful when the package alters the repo file during installation and thus would break idempotency, e.g. Google Chrome. |
| `except` | no | `clamav` | Avoid installing `package` on systems where this package is installed. Only supported on Debian derivatives. |
| `install_recommends` | no | `false` | By default, recommended dependencies are installed. This instructs apt to don't do that. Only supported on Debian derivatives. |

You must specify either:

- `gpg_url`
- `gpg_file`
- `gpg_server` and `gpg_id`

## Examples

```yml
- include_role:
    name: bviktor.thirdparty
  vars:
    name: 'Defender ATP'
    gpg_url: 'https://packages.microsoft.com/keys/microsoft.asc'
    repo_file: 'microsoft-prod'
    package: 'mdatp'
    install_recommends: false

- include_role:
    name: bviktor.thirdparty
  vars:
    name: 'Vulkan SDK'
    gpg_url: 'https://packages.lunarg.com/lunarg-signing-key-pub.asc'
    repo_file: 'lunarg-vulkan'
    package: 'vulkan-sdk'
    ldconfig: true
```

## Return Values

N/A

## Support

| Platform | Support | Status |
|---|---|---|
| Linter | ✅ | [![Lint](https://github.com/noobient/ansible-thirdparty/actions/workflows/lint.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/lint.yml) |
| AlmaLinux 8 | ✅ | [![AlmaLinux 8](https://github.com/noobient/ansible-thirdparty/actions/workflows/almalinux-8.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/almalinux-8.yml) |
| AlmaLinux 9 | ✅ | [![AlmaLinux 9](https://github.com/noobient/ansible-thirdparty/actions/workflows/almalinux-9.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/almalinux-9.yml) |
| Fedora 36 | ✅ | [![Fedora 36](https://github.com/noobient/ansible-thirdparty/actions/workflows/fedora-36.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/fedora-36.yml) |
| Ubuntu 18.04 | ✅ | [![Ubuntu 18.04](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-18.04.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-18.04.yml) |
| Ubuntu 20.04 | ✅ | [![Ubuntu 20.04](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-20.04.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-20.04.yml) |
| Ubuntu 22.04 | ✅ | [![Ubuntu 22.04](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-22.04.yml/badge.svg)](https://github.com/noobient/ansible-thirdparty/actions/workflows/ubuntu-22.04.yml) |
