# Helm In Docker

Package, install and upgrade helm charts with docker!

The [dipsas/helm](https://hub.docker.com/repository/docker/dipsas/helm) image includes helm and kubectl binaries, and makes it possible to package, install and upgrade helm charts inside of a container.
In addition, it is built on top of the [python](https://hub.docker.com/_/python) docker image, so that it is possible to execute a python script instead of a shell script.

## Example
`$PWD` is your full present working directory path.

### Package chart:
```
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm helm package my-helm-chart
```
Hint: Push a chart with [DockerFeed](https://github.com/DIPSAS/DockerFeed/tree/master/DockerFeedInDocker).

### Check kubectl config
```
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm kubectl config view
```

### Install chart in docker-desktop kubernetes
Change kubectl config in [./charts/.kube/config](./charts/.kube/config) with your own kube config.
Usually you can find your personal kube config with docker desktop on windows at:
- C:\\Users\\my-user\\.kube\\config
```
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm helm install my-helm-chart ./my-helm-chart
```

### Install charts in docker-desktop kubernetes with a shell script
Change kubectl config in [./charts/.kube/config](./charts/.kube/config) with your own kube config.
Usually you can find your personal kube config with docker desktop on windows at:
- C:\\Users\\my-user\\.kube\\config

Note! It is possible to execute a [python](https://www.python.org/) script instead if a shell script.
```
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm ./install.sh
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm ./upgrade.sh
docker run -it -v $PWD/charts/:/charts -w /charts dipsas/helm ./uninstall.sh
```
The nginx in [./charts/my-helm-chart](./charts/my-helm-chart) will be reachable on:
- https://my-helm-chart.localhost

## Development
- Requirements:
  - python & pip
    - https://www.python.org/
  - pip install DockerBuildManagement
    - https://github.com/DIPSAS/DockerBuildManagement

- Build & Publish
```
dbm -build -publish
```