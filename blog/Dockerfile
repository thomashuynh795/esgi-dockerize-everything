# Créer un Dockerfile pour cette application en mode production
FROM rustlang/rust:nightly

WORKDIR /src
COPY . .

RUN cargo install --path .
RUN cp /usr/local/cargo/bin/blog ./blog

RUN cargo install diesel_cli --no-default-features --features postgres
