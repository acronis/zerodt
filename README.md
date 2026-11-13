# ZeroDT

[![Go Reference](https://pkg.go.dev/badge/github.com/acronis/zerodt.svg)](https://pkg.go.dev/github.com/acronis/zerodt)
[![Build Status](https://github.com/acronis/zerodt/actions/workflows/go.yml/badge.svg)](https://github.com/acronis/zerodt/actions/workflows/go.yml)

Package `ZeroDT` offers a zero downtime restart and a graceful shutdown for HTTP servers. Key features:

* supported both stateless and stateful servers
* compatible with `systemd's` socket activation
* based on out-of-the-box `http.Server`
* work with any number of servers
* not a framework

## Example

The simplest way to use `ZeroDT` is to pass your `http.Server` to the `zerodt.NewApp` function and call `zerodt.ListenAndServe` for an object it returns:

```go
package main

import (
    "io"
    "net/http"
    "time"

    "github.com/acronis/zerodt"
)

func hello(w http.ResponseWriter, r *http.Request) {
    io.WriteString(w, "Hello world!")
}

func main() {
    mux := http.NewServeMux()
    mux.HandleFunc("/", hello)

    a := zerodt.NewApp(&http.Server{Addr: ":8081", Handler: mux})
    a.ListenAndServe()
}
```

## Adopting your HTTP server to use as `systemd's` service

Under construction
