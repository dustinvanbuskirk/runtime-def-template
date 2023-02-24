# internal-runtime-def

## Getting Started

1. Fork this repository
1. Clone your fork
1. See script usage below and run from local machine (you may need to chmod +x the image-import.sh)

## Image Helper Script

What does the script do?

It processes a list of public images.
Pulls those to your local machine.
Pushes them up to your private registry.
Updates all images to use your private registry.
Updates all files to point to your fork.

`./image-import.sh -i image-list-0.1.20.txt -r myregistry.codefresh.io/codefresh-poc -g "git_org/git_repo" -d true`

`-i image-list-0.1.20.txt` is the original image list found in this repository.

`-r myregistry.codefresh.io/codefresh-poc` is my docker registry domain and optional project to upload images

`-g "git_org/git_repo"` is my GIT repository where I fork this repository.

`-d true` is to give me a dry-run that will show me the file changes I can expect in a file manifest_dryrun.log

When running without dry-run you will get backups of all changed files and also a full log output of all changes to the file manifest_updates.log

You can elect to do this all manually see file below.

After done commit changes back to your fork and run the command below.

Replacing git_org, and codefresh-runtime with your specific runtime name if you want.  This will be used to create a GIT repository in your GIT organization and also used as the installation namespace.

`cf runtime install codefresh-runtime --runtime-def https://raw.githubusercontent.com/git_org/runtime-def-template/main/manifests/runtime.yaml --repo https://github.com/git_org/codefresh-runtime`

## image list for runtime 0.1.20:
```
argo-cd
-------
quay.io/codefresh/argocd:v2.4.15-cap-CR-15677-rollout-rollback
quay.io/codefresh/applicationset:v0.4.2-CR-13254-remove-private-logs
ghcr.io/dexidp/dex:v2.35.3-distroless
quay.io/codefresh/redis:7.0.4-alpine

argo-events
-----------
quay.io/codefresh/argo-events:v1.7.2-cap-CR-14600
nats-streaming:0.22.1
natsio/prometheus-nats-exporter:0.8.0
natsio/prometheus-nats-exporter:0.9.1
natsio/nats-server-config-reloader:0.7.0
nats:2.8.1
nats:2.8.2
nats:2.8.1-alpine
nats:2.8.2-alpine

argo-rollouts
-------------
quay.io/codefresh/argo-rollouts:v1.2.0-cap-CR-10626

argo-workflows
--------------
quay.io/codefresh/argocli:v3.4-cap-CR-15902
quay.io/codefresh/argoexec:v3.4-cap-CR-15902
quay.io/codefresh/workflow-controller:v3.4-cap-CR-15902

app-proxy
---------
quay.io/codefresh/cap-app-proxy:1.2056.0
alpine:3.16

internal-router
---------------
nginx:1.22-alpine

sealed-secrets
--------------
quay.io/codefresh/sealed-secrets-controller:v0.17.5

tunnel-client
-------------
quay.io/codefresh/frpc:2022.10.09-b0811fd
```
