# ReadSeekerPool

## Overview

ReadSeekerPool is a Go package designed to manage a pool of `io.ReadSeeker` objects efficiently. It provides functionality to reuse these objects, optimizing memory and resource usage when working with data streams that require seeking and reading capabilities.

## Features

- **Efficient Resource Management**: Pools `io.ReadSeeker` objects to reduce memory allocations and improve performance.
- **Ease of Use**: Simplifies the management of `io.ReadSeeker` objects in your applications.
- **Compatibility**: Designed to work seamlessly with other Go packages and standard libraries.

## Installation

To install ReadSeekerPool, use `go get`:

```sh
go get github.com/zing22845/readseekerpool
```

## Usage

Here is a basic example of how to use ReadSeekerPool in your Go project:

```go
package main

import (
    "github.com/zing22845/readseekerpool"
    "os"
    "log"
)

func main() {
    // create s3 client
    s3Client := ...

    // define keys: keys is a series of slices of a file，that we can seek and read
    // We can read and seek through this series of slices just like reading one file
    keys := []string{
	"object_slice1",
	"object_slice2"}
    storageType := "s3"
    poolSize := 20
    rsp, err := readseekerpool.NewReadSeekerPool(
        storageType,
	poolSize,
	s3client,
	"bucket-name",
	keys)

    // Get a ReadSeeker from the pool
    rs, err := rsp.Get()
    if err != nil {
        log.Fatal(err)
    }
    defer rsp.Put(rs)

    // Use the ReadSeeker
    // ...

}
```

## Main API

### `NewReadSeekerPool(rsType string, poolSize int, params ...interface{}) (rsp *ReadSeekerPool, err error)`

Creates a new instance of `ReadSeekerPool`.

### `(p *ReadSeekerPool) Get() (io.ReadSeeker, error)`

Fetches a `ReadSeeker` from the pool. If the pool is empty, it creates a new one.

### `(p *ReadSeekerPool) Put(rs io.ReadSeeker)`

Returns a `ReadSeeker` to the pool for reuse.

## Contributing

Contributions are welcome! Please fork the repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/zing22845/readseekerpool/blob/main/LICENSE) file for details.

## Acknowledgements

Thanks to all contributors and the open-source community for their valuable input and feedback.

For more information, visit the [GitHub repository](https://github.com/zing22845/readseekerpool).

---

