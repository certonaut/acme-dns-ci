# acme-dns-ci

[![CI Status](https://github.com/certonaut/acme-dns-ci/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/certonaut/acme-dns-ci/actions/workflows/docker-publish.yml)
[![GHCR Image](https://img.shields.io/badge/image-ghcr.io/certonaut/acme--dns--ci-blue)](https://ghcr.io/certonaut/acme-dns-ci)
[![License: Apache-2.0](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)

**A minimal CI wrapper for [joohoi/acme-dns](https://github.com/joohoi/acme-dns), delivering up-to-date, multi-arch Docker images via GitHub Container Registry (GHCR).**

## ✨ Overview

This repository provides a lightweight continuous integration setup that periodically builds the latest version of `acme-dns` and publishes Docker images to [ghcr.io](https://ghcr.io).
While the upstream `acme-dns` project offers Docker images, they are only published to Docker Hub and are not frequently updated. This project bridges that gap with:

- ✅ **Frequent builds** to keep up with the latest `main` branch changes
- 📦 **GitHub Container Registry (GHCR)** support (specifically: much higher rate limits compared to Docker Hub without an account)
- 🧬 **Multi-architecture images** for `amd64` and `arm64` (possibly more in the future)

## 🐳 Image Details

The Docker image is published under:

```
ghcr.io/certonaut/acme-dns-ci
```

### Supported Architectures

- `linux/amd64`
- `linux/arm64`

Additional architectures may be supported in the future.

### Tags

| Tag | Description |
|-----|-------------|
| `latest` | Continuously built from the latest upstream `main`/`master` branch |
| `<commit-sha>` | SHA-tagged image matching the upstream commit |
| `v<version>` | Latest build for acme-dns upstream version `version` |
| `vX.Y+<short-sha>` | Tagged "dirty" commits based upon a tag |

## 🚀 Usage

You can use the image just like the upstream one:

```bash
docker run --rm --name acmedns                 \
 -p 53:53                                      \
 -p 53:53/udp                                  \
 -p 80:80                                      \
 -v /path/to/your/config:/etc/acme-dns:ro      \
 -v /path/to/your/data:/var/lib/acme-dns       \
 -d ghcr.io/certonaut/acme-dns-ci
```

To use a specific version or commit:

```bash
# Specific upstream version
docker run ghcr.io/certonaut/acme-dns-ci:v1.1

# Specific upstream commit
docker run ghcr.io/certonaut/acme-dns-ci:9fabc123

# Dirty version (commit after tag)
docker run ghcr.io/certonaut/acme-dns-ci:v1.0+9fabc12
```

> **Note:** This image mirrors the upstream repository as-is. For configuration and usage, refer to the [official acme-dns documentation](https://github.com/joohoi/acme-dns).

## 🔄 Update Frequency

Images are built on a schedule (currently weekly). This ensures the image stays current with the latest improvements, even if acme-dns doesn't publish new releases.

## 🤝 Contributing

This project is intentionally minimal. If you'd like to suggest additional features (e.g. other architectures or tags), feel free to [open an issue](https://github.com/certonaut/acme-dns-ci/issues) or [submit a pull request](https://github.com/certonaut/acme-dns-ci/pulls).

## 📜 License

This repository only contains CI workflows and wrapper logic and is licensed under the [Apache License 2.0](./LICENSE).  
The `acme-dns` source code remains under its [original license](https://github.com/joohoi/acme-dns/blob/master/LICENSE).
