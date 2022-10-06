FROM rust:1.60 as build

RUN USER=root cargo new --bin web_server \
WOKRDIR /web_server

COPY ./Cargo.lock ./Cargo.lock
COPY ./Cargo.toml ./Cargo.toml

RUN cargo build --release
RUN rm src/*.rs

COPY ./src ./src

RUN rm ./target/release/deps/web_server*
RUN cargo build --release

FROM debian:buster-slim
COPY --from=build /web_server/target/release/web_server .

CMD ["./web_server"]

