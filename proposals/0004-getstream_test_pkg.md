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
