# pkg/minikube/constants
pkg constants defines default values minikube will use later:
- APIServerName
- ClusterDNSDomain
- MinikubeHome
- DefaultMinipath:filepath.Join(homedir.HomeDir(), ".minikube")
- KubeconfigPath
- KubeconfigEnvVar
- MinikubeContext
- MinikubeEnvPrefix
- DefaultMachineName
- DefaultStorageClassProvisioner
- MountProcessFileName
- SupportedVMDrivers
- config for vm
```golang
DefaultKeepContext  = false
ShaSuffix           = ".sha256"
DefaultMemory       = 2048
DefaultCPUS         = 2
DefaultDiskSize     = "20g"
MinimumDiskSizeMB   = 2000
DefaultVMDriver     = "virtualbox"
DefaultStatusFormat = "minikube: {{.MinikubeStatus}}\n" +
    "cluster: {{.ClusterStatus}}\n" + "kubectl: {{.KubeconfigStatus}}\n"
DefaultAddonListFormat     = "- {{.AddonName}}: {{.AddonStatus}}\n"
DefaultConfigViewFormat    = "- {{.ConfigKey}}: {{.ConfigValue}}\n"
GithubMinikubeReleasesURL  = "https://storage.googleapis.com/minikube/releases.json"
KubernetesVersionGCSURL    = "https://storage.googleapis.com/minikube/k8s_releases.json"
DefaultWait                = 20
DefaultInterval            = 6
DefaultClusterBootstrapper = "localkube"
```
- ...