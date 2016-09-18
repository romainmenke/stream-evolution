# Moving Some Tests to a seperate pkg

### getstream_test

- These would serve as examples as well as Tests
- They cover the public interface and the API calls
- They are only modified on major version updates
- They enforce API stability

### internal tests

- These cover internal logic
- They are not tied to major version updates
- They do not communicate with getstream
- They are independent of config and env


Use a helper function to determine which tests to skip. This ensures that API tests are only run when a config is present.

```go
if configMissing() {
	t.Skip("config missing, running internal tests only")
}

func configMissing() bool {

	testAPIKey := os.Getenv("key")
	testAPISecret := os.Getenv("secret")
	_ = os.Getenv("token")
	testAppID := os.Getenv("app_id")
	testRegion := os.Getenv("region")

	if testAPIKey == "" || testAPISecret == "" || testAppID == "" || testRegion == "" {
		return true
	}
	return false
}
```
