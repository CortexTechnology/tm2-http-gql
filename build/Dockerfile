FROM golang:1.15-alpine as build
ARG GITHUB_TOKEN

RUN apk add git
RUN git config --global url."https://${GITHUB_TOKEN}:x-oauth-basic@github.com/CortexTechnology/".insteadOf "https://github.com/CortexTechnology/"

WORKDIR /build
COPY . .
RUN go build -o tm2-http-gql

FROM alpine

WORKDIR /root

COPY --from=build /build/tm2-http-gql .
COPY --from=build /build/config.toml .

ENTRYPOINT ./tm2-http-gql