# Rust docker onbuild

> Make rust build **simple** & **fast**

## Usage:

```Dockerfile
FROM shuataren/rust-onbuild:1.37.0 AS builder

FROM alpine:latest
COPY --from=builder /myapp/myapp .
CMD ["./myapp"]
```
