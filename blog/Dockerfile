# Créer un Dockerfile pour cette application en mode production
FROM rust:latest

WORKDIR /src
COPY . .

EXPOSE 8000

ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /usr/local/bin/wait-for-it.sh
RUN chmod +x /usr/local/bin/wait-for-it.sh

RUN rustup default nightly

RUN cargo install --path .
RUN cp /usr/local/cargo/bin/blog ./blog

RUN cargo install diesel_cli --no-default-features --features postgres

CMD ["sh", "-c", "/usr/local/bin/wait-for-it.sh db:5432 -t 60 -- diesel migration run && ./blog"]
