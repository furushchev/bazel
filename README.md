# bazel

Docker image that contains Bazel via Bazelisk.

## Quick Start

### Pull from GitHub Container Registry

```bash
# Pull latest
docker pull ghcr.io/furushchev/bazel:ubuntu-24.04
```

### Usage Examples

```bash
# Check Bazel version
docker run --rm ghcr.io/furushchev/bazel:ubuntu-24.04 version

# Build a project
docker run --rm -v $(pwd):/workspace -w /workspace \
  ghcr.io/furushchev/bazel:ubuntu-24.04 build //...

# Run tests
docker run --rm -v $(pwd):/workspace -w /workspace \
  ghcr.io/furushchev/bazel:ubuntu-24.04 test //...

# Interactive shell
docker run --rm -it -v $(pwd):/workspace -w /workspace \
  ghcr.io/furushchev/bazel:ubuntu-24.04 bash
```

## Building Locally

### Build for your platform

```bash
docker build -f Dockerfile.ubuntu -t bazel:latest .
```

### Build with custom versions

```bash
docker build -f Dockerfile.ubuntu \
  --build-arg BASE_VERSION=22.04 \
  --build-arg BAZELISK_VERSION=1.27.0 \
  -t bazel:custom .
```

### Multi-platform build

Enable multi-platform build:

```bash
docker run --privileged --rm tonistiigi/binfmt --install all
docker buildx create --use
```

Then build the image:

```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -f Dockerfile.ubuntu \
  -t bazel .
```

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Author

Yuki Furuta
