FROM rust:latest

RUN cargo install mdbook --no-default-features --features output --vers "^0.3.5"
RUN cargo install mdbook-toc

CMD ["mdbook", "build"]