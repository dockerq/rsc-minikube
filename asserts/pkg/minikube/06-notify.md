# pkg/minikube/notify
notify will check minikube version and notify user if localversion < onlineversion(get from online).
- getJson from url
- read version info from localfile
- write version info to localfile
- compare localversion and onlineversion
- notify(print update info) user to update minikube

## parse response body to struct
```golang
return json.NewDecoder(r.Body).Decode(target)
```

## write time to file
```golang
err := ioutil.WriteFile(path, []byte(inputTime.Format(timeLayout)), 0644)
```

## parse time from string
```golang
timeInFile, err := time.Parse(timeLayout, string(lastUpdateCheckTime))
```