# pkg/minikube/kubernetes_versions
pkg to get and validate kubernetes versions.

- GetK8sVersionsFromURL
Just as its name implies, this method get kubernetes versions from url.
- IsValidLocalkubeVersion
check if kubernetes version validate.
- PrintKubernetesVersions
- getJson
```golang
func getJson(url string, target *K8sReleases) error {
	r, err := http.Get(url)
	if err != nil {
		return errors.Wrapf(err, "Error getting json from url: %s via http", url)
	}
	defer r.Body.Close()

	return json.NewDecoder(r.Body).Decode(target)
}
```
get request from url and decode to target.