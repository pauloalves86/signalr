# Overview

This is my personal attempt at implementating the client side of the WebSocket
portion of the SignalR protocol. I use it for various virtual currency trading
platforms that use SignalR.

It supports CloudFlare-protected sites by default.

## Examples

Simple example:

```go
package main

import (
	"log"

	"github.com/pauloalves86/signalr"
)

func main() {
	// Prepare a SignalR client.
	c := signalr.New(
		"fake-server.definitely-not-real",
		"1.5",
		"/signalr",
		`[{"name":"awesomehub"}]`,
		nil,
	)

	// Define message and error handlers.
	msgHandler := func(msg signalr.Message) { log.Println(msg) }
	panicIfErr := func(err error) {
		if err != nil {
			log.Panic(err)
		}
	}

	// Start the connection.
	err := c.Run(msgHandler, panicIfErr)
	panicIfErr(err)

	// Wait indefinitely.
	select {}
}
```

Generic usage:

- [Basic usage](https://github.com/pauloalves86/signalr/blob/master/examples/basic/main.go)
- [Complex usage](https://github.com/pauloalves86/signalr/blob/master/examples/complex/main.go)

Cryptocurrency examples:

- [Bittrex](https://github.com/pauloalves86/signalr/blob/master/examples/bittrex/main.go)
- [Cryptopia](https://github.com/pauloalves86/signalr/blob/master/examples/cryptopia/main.go)

Proxy examples:

- [No authentication](https://github.com/pauloalves86/signalr/blob/master/examples/proxy-simple)
- [With authentication](https://github.com/pauloalves86/signalr/blob/master/examples/proxy-authenticated)

# Documentation

- GoDoc: https://godoc.org/github.com/pauloalves86/signalr
- SignalR specification: https://docs.microsoft.com/en-us/aspnet/signalr/overview/
- Excellent technical deep dive of the protocol: https://blog.3d-logic.com/2015/03/29/signalr-on-the-wire-an-informal-description-of-the-signalr-protocol/

# Contribute

If anything is unclear or could be improved, please open an issue or submit a
pull request. Thanks!
