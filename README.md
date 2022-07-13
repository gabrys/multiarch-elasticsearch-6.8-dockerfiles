This is a repo for multi-arch build of Elasticsearch 6.8

The multi-arch build is published to https://hub.docker.com/r/gabrys/elasticsearch

In order to build this image:

```
# Build:
$ cd elasticsearch
$ docker buildx build --tag gabrys/elasticsearch:6.8 .
```

In order to push to Docker Hub:

```
$ cd elasticsearch
# Log in to Docker Hub:
$ security -v unlock-keychain ~/Library/Keychains/login.keychain-db
$ docker login -u gabrys
$ docker buildx create --use
# Build and push:
$ docker buildx build --platform linux/arm64/v8,linux/amd64 --push --tag gabrys/elasticsearch:6.8 .
```

Changes vs official 6.8 branch:

https://github.com/gabrys/multiarch-elasticsearch-6.8-dockerfiles/compare/6.8...6.8-arm

1. Download the JDK for the detected architecture rather than always for x64
2. Remove `UseAVX=2` setting on non-x64
3. Add `xpack.ml.enabled: false` as it doesn't work outside x64
