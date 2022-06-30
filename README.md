# Chromium for linux/amd64,linux/arm64
This is my repo in order to create a docker image running a chromium headless instance for regression testing.
The image works on both arm and amd64 achitecture and is suitable for a seamless use with the library [docker-chromium](https://www.npmjs.com/package/docker-chromium), 
especially with my forked version available on [this repo and branch]()

In order to ease the automation of the generation of the image, a github action workflow is there for you:

- it builds the images for the platforms
- it pushes them on your own docker hub


## Github Workflow
First and foremost set your github secrets for the action. This way it will be able to push the generated images:

```
DOCKERHUB_USER
DOCKERHUB_PASSWORD
```

Then, set the environment variables needed to generate the proper image tag and push it to the proper docker hub repo:

.env file:
```
DOCKER_HUB_REPO=bertuz/docker-chromium
DOCKER_IMAGE_VERSION=chromium103.0.5060.53-1
```

Then you can launch it by executing:
```zsh
gh workflow run build-docker-image.yml --ref main
```
