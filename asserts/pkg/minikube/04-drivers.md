# pkg/minikube/drivers
I thought drivers pkg is very complex,but it only has on subpkg and few functions.
I think pkg drivers will have more functions.

## hyperkit/disk.go
- createDiskImage
this method needs github.com/docker/machine/libmachine/mcnutils。
it creates a file and write bytes to it.
- fixPermissions
just as its name implies, fis permissions of path.