# Options

### Background

https://commandcenter.blogspot.be/2014/01/self-referential-functions-and-design.html

> I've been trying on and off to find a nice way to deal with setting options in a Go package I am writing. Options on a type, that is. The package is intricate and there will probably end up being dozens of options. There are many ways to do this kind of thing, but I wanted one that felt nice to use, didn't require too much API (or at least not too much for the user to absorb), and could grow as needed without bloat.

> I've tried most of the obvious ways: option structs, lots of methods, variant constructors, and more, and found them all unsatisfactory. After a bunch of trial versions over the past year or so, and a lot of conversations with other Gophers making suggestions, I've finally found one I like. You might like it too. Or you might not, but either way it does show an interesting use of self-referential functions.

http://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis

Excerpt

> In summary

> Functional options let you write APIs that can grow over time.
They enable the default use case to be the simplest.
They provide meaningful configuration parameters.
Finally they give you access to the entire power of the language to initialize complex values.
In this talk, I have presented many of the existing configuration patterns, those considered idiomatic and commonly in use today, and at every stage asked questions like:

> - Can this be made simpler ?

> - Is that parameter necessary ?

> - Does the signature of this function make it easy for it to be used safely ?

> - Does the API contain traps or confusing misdirection that will frustrate ?

### Info

- the entry point of every golang pkg should be a `New` method.
- to avoid multiple functions that start with `New..` it is best pass a slice of mutating functions as a variadic parameter.
- config structs that mirror the type they help construct are duplicates of the `Type{}` pattern.
- default implementations of Option functions can be easily defined.  


```go
type Option func(*Client)

// single param option
func Secret(secret string) Option {
	return func(c *Client) {
		c.Secret = secret
	}
}

// more complex option
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
