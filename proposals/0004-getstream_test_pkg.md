# Moving Some Tests to a seperate pkg

### getstream_test

- These would serve as examples as well as Tests
- They only Cover the public interface
- They are only modified on major version updates
- They enforce API stability

### internal tests

- These cover the entire pkg
- They are not tied to major version updates
