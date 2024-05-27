# Flag

todo

## Example

source `example.go`:

``` go
package main

import (
    "flag"
    "fmt"

    "github.com/m4gshm/flag/flagenum"
)

func main() {
    var (
        api = flagenum.MultipleStrings(
            "api",
            []string{"rest", "grpc"}/*default*/,
            []string{"rest", "grpc", "soap"}/*allowed*/,
            "enabled api engine",
        )
        logLevel = flagenum.SingleString(
            "log-level",
            "info"/*default*/,
            []string{"debug", "info", "warn", "error"}/*allowed*/,
            "logger level",
        )
    )
    flag.Parse()

    fmt.Printf("enabled apis: %v\n", *api)
    fmt.Printf("log level:    %s\n", *logLevel)
}
```

Command `go run .` will print:

``` console
enabled apis: [rest grpc]
log level:    info
```

To change defaults need set arguments like
`go run . --api soap --api rest --log-level debug`

``` console
enabled apis: [soap rest]
log level:    debug
```

Call `go run . --help` to get usage info:

``` console
Usage of example:
  -api value
        enabled api engine (allowed: [rest grpc soap]) (default [rest grpc])
  -log-level value
        logger level (allowed: [debug info warn error]) (default info)
```