# Client Clean Up

- `baseURL` would be removed from `Client`
- `Version` would be added
- `BaseURL()` would be added

`BaseURL` should follow changes made to `Client` params and should not be set fixed on construction.

```go
// Client is used to connect to getstream.io
type Client struct {
	ID       string
	Key      string
	Location string
	Secret   string
	Token    string
	Version  string

	HTTP    *http.Client
	Signer  *Signer
}

func (c *Client) BaseURL() (*url.URL, error) {
	baseURLStr := "https://api.getstream.io/api/v1.0/"
	if c.Location != "" {
		baseURLStr = "https://" + c.Location + "-api.getstream.io/api/" + c.Version + "/"
	}

	baseURL, err := url.Parse(baseURLStr)
	if err != nil {
		return nil, err
	}

	return baseURL, nil
}
```
