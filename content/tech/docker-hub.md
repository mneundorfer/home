---
title: "Docker Push"
date: 2018-04-02T10:01:29+02:00
draft: true
tags: ["docker", "hub", "arm", "x64", "automated", "build"]
---

# DockerHub Notes

## Automated Builds

You can set up automated builds based on GitHub repos. This, however, does only work for `x64` based images, as the DockerHub infrastructure does not support building `arm`! These images therefore have to be built locally and then pushed to the registry.

## Push Images to DockerHub

```bash
$ docker login
> NAME
> PASS

docker tag imagetobepushed:latest DOCKER_ID/imagetobepushed
docker push DOCKER_ID/imagetobepushed
```

## Build Failing

No build is triggered --> `Unexpected Error`, no logs.

--> Trigger the build via a push on the GitHub repo, *not* via the `Trigger` function in the `Build Details`. Also, *first* define tags in the `Build Details`, *then* tag and push on GitHub.