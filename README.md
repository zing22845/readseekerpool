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
    pool := readseekerpool.New()

    // Open a file
    file, err := os.Open("example.txt")
    if err != nil {
        log.Fatal(err)
    }
    defer file.Close()

    // Get a ReadSeeker from the pool
    rs, err := pool.Get(file)
    if err != nil {
        log.Fatal(err)
    }

    // Use the ReadSeeker
    // ...

    // Put the ReadSeeker back into the pool
    pool.Put(rs)
}
```

## API

### `New() *ReadSeekerPool`

Creates a new instance of `ReadSeekerPool`.

### `Get(rs io.ReadSeeker) (io.ReadSeeker, error)`

Fetches a `ReadSeeker` from the pool. If the pool is empty, it creates a new one.

### `Put(rs io.ReadSeeker)`

Returns a `ReadSeeker` to the pool for reuse.

## Contributing

Contributions are welcome! Please fork the repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/zing22845/readseekerpool/blob/main/LICENSE) file for details.

## Acknowledgements

Thanks to all contributors and the open-source community for their valuable input and feedback.

For more information, visit the [GitHub repository](https://github.com/zing22845/readseekerpool).

---

