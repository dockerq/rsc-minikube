# Build and Test
Read source code of [minikube](https://github.com/kubernetes/minikube)

## Build from source code
First, you need go 1.8+ and set GOPATH and GOROOT correctlly.Then, clone code:
```shell
git clone https://github.com/kubernetes/minikube.git $GOPATH/src/k8s.io
```
If you want to save time, you can add `--depth=1` to git:
```shell
git clone --depth=1 https://github.com/kubernetes/minikube.git $GOPATH/src/k8s.io
```
Then, build with default instruction `make`:
```shell
cd $GOPATH/src/k8s.io/minikube
make
```

## Test minikube code
There are three kinds of test:
- Unit test: `make test`, test atomic program function or method.
- Integration test: `make integration`, test across function or method all invoke path.
- Conformance test: refer to [minikube conformance test](https://github.com/kubernetes/minikube/blob/master/docs/contributors/build_guide.md#conformance-tests).

Below is output of compile:
```shell
➜  minikube git:(master) time make
CGO_ENABLED=1 go build -tags static_build -ldflags="-X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitCommit=17d7182a7ccbb167074be7a87f0a68bd00d58d97 -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitVersion=v1.7.5 -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitTreeState=clean -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.buildDate=2017-09-24T23:02:53Z -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitCommit=17d7182a7ccbb167074be7a87f0a68bd00d58d97 -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitVersion=v1.7.5 -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitTreeState=clean -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.buildDate=2017-09-24T23:02:53Z  -X k8s.io/minikube/pkg/version.version=v0.22.2 -X k8s.io/minikube/pkg/version.isoVersion=v0.23.4 -X k8s.io/minikube/pkg/version.isoPath=minikube/iso -s -w -extldflags '-static'" -o ./out/localkube ./cmd/localkube
# k8s.io/minikube/cmd/localkube
/usr/local/golang/versions/go1.8.1/go/pkg/tool/linux_amd64/link: running gcc failed: fork/exec /usr/bin/gcc: cannot allocate memory

Makefile:104: recipe for target 'out/localkube' failed
make: *** [out/localkube] Error 2
make  516.20s user 42.63s system 147% cpu 6:18.56 total
```

Below is output of unit test:
```shell
➜  minikube git:(master) time make test
CGO_ENABLED=1 go build -tags static_build -ldflags="-X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitCommit=17d7182a7ccbb167074be7a87f0a68bd00d58d97 -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitVersion=v1.7.5 -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.gitTreeState=clean -X k8s.io/minikube/vendor/k8s.io/kubernetes/pkg/version.buildDate=2017-09-24T22:43:56Z -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitCommit=17d7182a7ccbb167074be7a87f0a68bd00d58d97 -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitVersion=v1.7.5 -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.gitTreeState=clean -X k8s.io/minikube/vendor/k8s.io/client-go/pkg/version.buildDate=2017-09-24T22:43:56Z  -X k8s.io/minikube/pkg/version.version=v0.22.2 -X k8s.io/minikube/pkg/version.isoVersion=v0.23.4 -X k8s.io/minikube/pkg/version.isoPath=minikube/iso -s -w -extldflags '-static'" -o ./out/localkube ./cmd/localkube
# k8s.io/minikube/cmd/localkube
/usr/local/golang/versions/go1.8.1/go/pkg/tool/linux_amd64/link: running gcc failed: fork/exec /usr/bin/gcc: cannot allocate memory

Makefile:104: recipe for target 'out/localkube' failed
make: *** [out/localkube] Error 2
make test  476.86s user 41.29s system 120% cpu 7:09.00 total
```
Because my machine does not have enough **memory** so compile and unit test both fail.

## Conclusion
Compile minikube will pull image from gcr.io, so your machine is supporsed to access gcr.io. If not, you will fail.

Both test and compile need **4GB+ memory**.