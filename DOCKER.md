# Docker Setup for OpenPLC v3

This fork includes automatic Docker image building for arm64 architecture via GitHub Actions.

## Using the Docker Image

### Pull the latest image:
```bash
docker pull ghcr.io/smilexs4/openplc_v3:latest
```

### Run the container:
```bash
docker run -d \
  -p 8080:8080 \
  -v openplc_data:/docker_persistent \
  --name openplc \
  ghcr.io/smilexs4/openplc_v3:latest
```

### Access the web interface:
Open your browser and navigate to: `http://localhost:8080`

Default credentials:
- Username: `openplc`
- Password: `openplc`

## Available Tags

- `latest` - Latest build from the master branch
- `master` - Latest build from the master branch
- `<commit-sha>` - Specific commit builds

## Architecture Support

Currently supported:
- `linux/arm64`

To add more architectures (amd64, arm/v7, etc.), edit `.github/workflows/docker-build.yml` line 62 and update the `platforms` field.

## Automatic Builds

The Docker image is automatically rebuilt when:
- Code is pushed to `master`, `main`, or `develop` branches
- A pull request is created
- Manually triggered via GitHub Actions

## Persistent Storage

The container uses a volume mounted at `/docker_persistent` to store:
- Configuration files
- Database
- ST program files
- Active program state

To backup your data:
```bash
docker cp openplc:/docker_persistent ./backup
```

## Viewing Logs

```bash
docker logs openplc
```

## Stopping the Container

```bash
docker stop openplc
docker rm openplc
```
