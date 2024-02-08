# LeapfrogAI Model Skeleton

This Zarf package contains the foundational configuration required to deploy a model backend to a Kubernetes cluster hosting LeapfrogAI.

This repository is a dedicated [skeleton Zarf Package](https://docs.zarf.dev/docs/faq#what-is-a-skeleton-zarf-package). The published skeleton artifact for this repo can be found [here](https://github.com/defenseunicorns/leapfrog-model-skeleton/pkgs/container/packages%2Fleapfrogai%2Fleapfrogai-model).

## Examples

Some example repositories that use this skeleton are:

- [defenseunicorns/llama-cpp-python](https://github.com/defenseunicorns/leapfrogai-backend-llama-cpp-python)
- [defenseunicorns/whisper](https://github.com/defenseunicorns/leapfrogai-backend-whisper)

## Publishing a Package

A workflow already automatically deploys a new package at every tag push, but the manual way to do it is as follows:

```bash
zarf package publish . ghcr.io/defenseunicorns/packages/leapfrogai/leapfrogai-model:<IMAGE_TAG>
```

## Testing a Package

To test a package locally, you first need a running cluster and an example model backend to be tested. After those are in place, execute the following:

```bash
# create a local registry
docker run -d -p 5000:5000 --restart=always --name registry registry:2

# publish the skeleton to the local registry
zarf package publish . oci://localhost:5000/defenseunicorns/packages/leapfrogai --insecure

# create model backend package using local skeleton
# this example will use leapfrogai-backend-whisper
# edit the import-model componenet to use image: localhost:5000/defenseunicorns/packages/leapfrogai/leapfrogai-model:<IMAGE_TAG>
zarf package create --insecure
```
