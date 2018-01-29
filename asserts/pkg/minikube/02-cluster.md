# pkg/minikube/cluster
Cluster pkg operates the VM and k8s cluster.It defines MachineConfig and Config which holds `MachineConfig` and `bootstrapper.KubernetesConfig`.

Cluster has below important methods

## cluster.go
### StartHost
This method needs libmachine api and MachineConfig.
1. check if VM machine exists, if not, create and return it.
2. if vm exists, load it as host, then check host status.
    - if host does not running, starts host and save host status.
3. if host driver is "none", run `h.ConfigureAuth()`
4. finally, return host and nil(error).

### StopHost
Load host uses libmachine api and stops it.

### DeleteHost
Load host uses libmachine api and deletes it.
While deleting host it maybe run into many errors,so we use `MultiError` to handle process of deleting.

### GetHostStatus
1. check if host exists, if not, return none status.
2. load host and get status using host driver api.
3. return status in step 2.

### GetHostDriverIP
1. load host and get ip using driver api.
2. parse and return ip.

### createVirtualboxHost
return virtualbox dirver

### createHost
receive libmachine.API and MachineConfig as parameters.
It will switch MachineConfig.VMDriver, creates host driver according to driver kinds.
Although driver type is ensure,run `h, err := api.NewHost(config.VMDriver, data)` to get a host struct.
Config host --> create host --> save host.

### GetHostDockerEnv
get host and then get dirver ip,parse ip to docker env map.

### MountHost
runs the mount command from the 9p client on the VM to the 9p server on the host.
**so what is 9p client and 9p server?**

### CreateSSHShell
1. get host.
2. check vm host(cluster) status,if not running, return error.
3. create ssh client use host: `client, err := host.CreateSSHClient()`.
4. run client with args `client.Shell(args...)`.


## different platforms
1. cluster_windows.go
    - createHypervHost
2. cluster_linux.go
    - createKVMHost
3. cluster_darwin.go
    - createXhyveHost
    - createHyperkitHost

## Conclusion
cluster mainly provides methods to operates cluster:
- create
- start
- stop
- delete
- ...
It also supports different method according to platform: windows,linux and darwin.