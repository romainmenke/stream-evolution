# Remove FeedID type

`FeedID` was useful for me as a way to enforce the `string` format where needed. This however is not clear to users of the package as they can just cast any `string` to `FeedID`.

So I propose remove the `FeedID` type and replacing it with `string`. Functions and Methods that take a `FeedID` format should validate their input and return errors when validation fails.
