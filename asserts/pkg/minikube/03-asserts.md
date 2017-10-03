# pkg/minikube/asserts

## addons.go
addons defines components and their yaml,manifests files for minikube:
- addon-manager
- dashboard
- default-storageclass
- kube-dns
- heapster
- ingress
- registry
- registry-creds

the yaml file is for kubenetes to create pods or deployments/services.

## vm_asserts.go
support a base assert struct and interfaces:
```golang
type CopyableFile interface {
	io.Reader
	GetLength() int
	GetAssetName() string
	GetTargetDir() string
	GetTargetName() string
	GetPermissions() string
}

type BaseAsset struct {
	data        []byte
	reader      io.Reader
	Length      int
	AssetName   string
	TargetDir   string
	TargetName  string
	Permissions string
}
```
Then implements below two assert struct:
- MemoryAsset
- BinDataAsset
they are for vm to use.