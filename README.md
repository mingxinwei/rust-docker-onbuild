# Rust docker onbuild

> Make rust docker build **simple** & **fast** 🚀

## Features

- Leverage docker cache to make image build as fast as possible.
- Generate small image.
- Make it easy to write your project's Dockerfile.

## Usage

```Dockerfile
# First stage build
FROM shuataren/rust-onbuild:1.37.0 AS builder

# Second stage which generates the final small image
FROM alpine:latest
COPY --from=builder /myapp/myapp .
CMD ["./myapp"]
```
