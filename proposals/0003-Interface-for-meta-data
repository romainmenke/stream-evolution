# map[string]interface{} for Meta Data

Using `interface{}` for Meta Data will allow more flexible usage of top level key/value pairs.

```go
type Activity struct {
	ID        string
	Actor     FeedID
	Verb      string
	Object    FeedID
	Target    FeedID
	Origin    FeedID
	TimeStamp *time.Time

	ForeignID string
	Data      *json.RawMessage
	MetaData  map[string]interface{}

	To []Feed
}
```
