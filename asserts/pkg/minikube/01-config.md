# pkg/minikube/config
This pkg is simple, it is mainly for MinikubeConfig `type MinikubeConfig map[string]interface{}`.
MinikubeConfig is a map, its value is interface.Main function about it is:
```golang
// ReadConfig reads in the JSON minikube config
func ReadConfig() (MinikubeConfig, error) {
	f, err := os.Open(constants.ConfigFile)
	if err != nil {
		if os.IsNotExist(err) {
			return make(map[string]interface{}), nil
		}
		return nil, fmt.Errorf("Could not open file %s: %s", constants.ConfigFile, err)
	}
	m, err := decode(f)
	if err != nil {
		return nil, fmt.Errorf("Could not decode config %s: %s", constants.ConfigFile, err)
	}

	return m, nil
}
```