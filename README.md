# Rust docker onbuild

> Make rust build **simple** & **fast**

## Usage:

```Dockerfile
FROM shuataren/rust:1.37.0-onbuild AS builder

FROM alpine:latest
COPY --from=builder /myapp/myapp .
CMD ["./myapp"]
```
