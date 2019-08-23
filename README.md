# Rust docker onbuild

> Make rust build **simple** & **fast** 🚀

## Usage:

```Dockerfile
# Fist stage build
FROM shuataren/rust-onbuild:1.37.0 AS builder

# Final image
FROM alpine:latest
COPY --from=builder /myapp/myapp .
CMD ["./myapp"]
```
