FROM rust:1.37.0

RUN apt-get update
RUN apt-get install musl-tools -y

RUN rustup target add x86_64-unknown-linux-musl

RUN USER=root cargo new myapp
WORKDIR /myapp

ONBUILD COPY Cargo.toml Cargo.lock ./ 
ONBUILD RUN sed -n 's/name = "\(.*\)"/\1/p' Cargo.toml > /tmp/BIN_NAME
# If Cargo.toml name contains '-', will be translated into '_' in target/<triple>/release/deps/
ONBUILD RUN sed 's/-/_/g' /tmp/BIN_NAME > /tmp/DEP_NAME_PREFIX

# Download and (pre)build the dependency, leverage the docker cache mechanism to speed up build when toml & lock file not changed
ONBUILD RUN cargo build --release --target=x86_64-unknown-linux-musl
ONBUILD RUN rm target/x86_64-unknown-linux-musl/release/deps/$(cat /tmp/DEP_NAME_PREFIX)*

# Build the real code
ONBUILD COPY . .
ONBUILD RUN cargo build --release --target=x86_64-unknown-linux-musl
ONBUILD RUN mv target/x86_64-unknown-linux-musl/release/$(cat /tmp/BIN_NAME) ./myapp
