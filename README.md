# Laravel K8s

An API built on Laravel and Kubernetes.

## Resources

- [‘Bosun Egberinde Laracon  US '22](https://www.youtube.com/watch?v=f4QShF42c6E)
- [Kubernetes for Laravel](https://kubernetesforlaravel.com/)
- [Load Images into Kind](https://iximiuz.com/en/posts/kubernetes-kind-load-docker-image/)
- [Use Ingress with Kind](https://dustinspecker.com/posts/test-ingress-in-kind/)

## Local Development

Build
```sh
docker build --platform linux/arm64 . --tag=basic-app # add platform flag for kind
docker build src -t basic-app
```

Load Image
```sh
kind load docker-image basic-nginx:latest
````

View
```sh
open localhost:8787
```

## Deploy

```sh
echo $REPLICATED_APP # make sure you env is set
docker build src -t registry.replicated.com/$REPLICATED_APP/basic-app:1.0.0
docker push registry.replicated.com/$REPLICATED_APP/basic-app:1.0.0
```
