# Options

### Info

- the entry point of every golang pkg should be a `New` method.
- to avoid multiple functions that start with `New..` it is best pass a slice of mutating functions as a variadic parameter.
- config structs that mirror the type they help construct are duplicates of the `Type{}` pattern.
- default implementations of Option functions can be easily defined.  


```go
type Option func(*Client)

func ServerOptions(key string, secret string, appID string, location string) Option {
	return func(c *Client) {
		c.Key = key
		c.Secret = secret
		c.AppID = appID
		c.Location = location
	}
}

func ClientOptions(key string, token string, appID string, location string) Option {
	return func(c *Client) {
		c.Key = key
		c.Token = token
		c.AppID = appID
		c.Location = location
	}
}

func New(options ...Option) *Client {
	c := Client{}

	for _, opt := range options {
		opt(&c)
	}

	return &c

}
```
