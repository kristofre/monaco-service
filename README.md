# README

This is a Sandbox Keptn Services that enables calling the Dynatrace Monaco (Monitoring as Code) toolset for individual Keptn Events

For more information on Dynatrace Monaco, visit the git repository https://github.com/dynatrace-oss/dynatrace-monitoring-as-code

---

# monaco-service
![GitHub release (latest by date)](https://img.shields.io/github/v/release/keptn-sandbox/monaco-service)
[![Go Report Card](https://goreportcard.com/badge/github.com/keptn-sandbox/monaco-service)](https://goreportcard.com/report/github.com/keptn-sandbox/monaco-service)

This implements a monaco-service for Keptn. If you want to learn more about Keptn visit us on [keptn.sh](https://keptn.sh)

## Compatibility Matrix

*Please fill in your versions accordingly*

| Keptn Version    | [monaco-service Docker Image](https://hub.docker.com/r/keptnsandbox/monaco-service/tags) |
|:----------------:|:----------------------------------------:|
|       0.7.3      | keptnsandbox/monaco-service:0.1.0 |

## Installation

The *monaco-service* can be installed as a part of [Keptn's uniform](https://keptn.sh).

### Deploy in your Kubernetes cluster

To deploy the current version of the *monaco-service* in your Keptn Kubernetes cluster, apply the [`deploy/service.yaml`](deploy/service.yaml) file:

```console
kubectl apply -f deploy/service.yaml
```

This should install the `monaco-service` together with a Keptn `distributor` into the `keptn` namespace, which you can verify using

```console
kubectl -n keptn get deployment monaco-service -o wide
kubectl -n keptn get pods -l run=monaco-service
```

### Up- or Downgrading

Adapt and use the following command in case you want to up- or downgrade your installed version (specified by the `$VERSION` placeholder):

```console
kubectl -n keptn set image deployment/monaco-service monaco-service=keptnsandbox/monaco-service:$VERSION --record
```

### Uninstall

To delete a deployed *monaco-service*, use the file `deploy/*.yaml` files from this repository and delete the Kubernetes resources:

```console
kubectl delete -f deploy/service.yaml
```

## Usage

The goal of the *monaco-service* is to allow the user to trigger Dynatrace Monaco as part of their keptn-driven releases. 




## Development

This is an open source project, so I welcome any contributions to make it even better!

### Where to start

If you don't care about the details, your first entrypoint is [eventhandlers.go](eventhandlers.go). Within this file 
 you can add implementation for pre-defined Keptn Cloud events.
 
To better understand Keptn CloudEvents, please look at the [Keptn Spec](https://github.com/keptn/spec).
 
If you want to get more insights, please look into [main.go](main.go), [deploy/service.yaml](deploy/service.yaml),
 consult the [Keptn docs](https://keptn.sh/docs/) as well as existing [Keptn Core](https://github.com/keptn/keptn) and
 [Keptn Contrib](https://github.com/keptn-contrib/) services.

### Build yourself

* Build the binary: `go build -ldflags '-linkmode=external' -v -o monaco-service`
* Run tests: `go test -race -v ./...`
* Build the docker image: `docker build . -t keptnsandbox/monaco-service:dev` (Note: Ensure that you use the correct DockerHub account/organization)
* Run the docker image locally: `docker run --rm -it -p 8080:8080 keptnsandbox/monaco-service:dev`
* Push the docker image to DockerHub: `docker push keptnsandbox/monaco-service:dev` (Note: Ensure that you use the correct DockerHub account/organization)
* Deploy the service using `kubectl`: `kubectl apply -f deploy/`
* Delete/undeploy the service using `kubectl`: `kubectl delete -f deploy/`
* Watch the deployment using `kubectl`: `kubectl -n keptn get deployment monaco-service -o wide`
* Get logs using `kubectl`: `kubectl -n keptn logs deployment/monaco-service -f`
* Watch the deployed pods using `kubectl`: `kubectl -n keptn get pods -l run=monaco-service`
* Deploy the service using [Skaffold](https://skaffold.dev/): `skaffold run --default-repo=your-docker-registry --tail` (Note: Replace `your-docker-registry` with your DockerHub username; also make sure to adapt the image name in [skaffold.yaml](skaffold.yaml))


### Testing Cloud Events

We have dummy cloud-events in the form of [RFC 2616](https://ietf.org/rfc/rfc2616.txt) requests in the [test-events/](test-events/) directory. These can be easily executed using third party plugins such as the [Huachao Mao REST Client in VS Code](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).


## License

Please find more information in the [LICENSE](LICENSE) file.
