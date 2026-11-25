## Dockerfiles
```shell
# Building Docker images
docker image build -f path/to/Dockerfile -t image-name:tag .

# Clearing Docker build cache
docker builder prune -a

# Scanning Dockerfiles using Checkov
docker compose run --rm checkov \
  --framework dockerfile \
  -f /workspace/path/to/Dockerfile
```
