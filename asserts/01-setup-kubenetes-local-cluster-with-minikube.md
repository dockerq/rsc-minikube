# Set up kubenetes local cluster with minikube

## Install minikube and kubectl
Refer to [installations](https://github.com/kubernetes/minikube#installation) to install dependencies.

## Start
```shell
minikube start --vm-driver=xhyve # vm dirver is needed on MacOS
```
**Note**: Your machine must access to `gcr.io` and some other sites (across the GFW).Because minikube will try to pull needed image from gcr.io . If you can't access to gcr.io, you will not set up your cluster even though `minikube status` or `kubectl cluster-info` work well.

Run `minikube dashboard`, if your default browser can open portal of k8s cluster, you start success.

## Conclusion
Your machine must access gcr.io.