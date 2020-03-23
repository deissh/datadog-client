# datadog-client

> ***do not use in production***

a wrapper over the [datadog-go/statsd](http://github.com/DataDog/datadog-go/statsd) which can reconnect when a connection is lost

## Example

```bash
$ go get -u github.com/deissh/datadog-client
```

```go
package main

import (
	dc "github.com/deissh/datadog-client"
	"time"
)

func main() {
	// creating new connection to 127.0.0.1:8125
	dc.InitializeClient()
	// set prefix to all events, messages, metrics and etc
	dc.SetPrefix("someprefix_")
	// set tags
	dc.AddTag("debug", "true")
	dc.AddTag("version", "v1.2.3")
	
	// creating a gauge task that will running every minute
	dc.RunGaugeTask(
		"user_online",
		time.Minute,
		dc.Tags{},
		func() (f float64, err error) {
			return 5, err
		},
	)
	
	// start client updater
	dc.Start()
	// or run in goroutine dc.Start()
}
```
