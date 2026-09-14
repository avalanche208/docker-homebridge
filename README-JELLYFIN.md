# Homebridge with Jellyfin FFmpeg

This fork tracks [homebridge/docker-homebridge](https://github.com/homebridge/docker-homebridge) and publishes a derived Homebridge image containing the official Jellyfin FFmpeg Debian package.

## Images

- `ghcr.io/avalanche208/homebridge-jellyfin-ffmpeg:latest`
- `avalanche208/homebridge-jellyfin-ffmpeg:latest` (when Docker Hub secrets are configured)

Supported architectures: `linux/amd64` and `linux/arm64`. Jellyfin does not publish the required Ubuntu Noble package for ARMv7.

## Docker Compose

```yaml
services:
  homebridge:
    image: avalanche208/homebridge-jellyfin-ffmpeg:latest
    restart: unless-stopped
    network_mode: host
    volumes:
      - /path/to/homebridge:/homebridge
    environment:
      TZ: America/Chicago
```

## Automatic updates

The GitHub Actions workflow runs every Sunday. It merges the official repository's `latest` branch, pulls the newest official `homebridge/homebridge:latest` base image, and rebuilds this image. It can also be run manually from the Actions tab.

Docker Hub publishing requires these repository secrets:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

GHCR publishing uses GitHub's built-in token and requires no Docker Hub credentials.

## Verify FFmpeg

```bash
docker run --rm --entrypoint ffmpeg \
  avalanche208/homebridge-jellyfin-ffmpeg:latest -version
```

The executable is available at both `/usr/lib/jellyfin-ffmpeg/ffmpeg` and `/usr/local/bin/ffmpeg`.
