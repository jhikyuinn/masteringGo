### Bulder
FROM golang:1.19.0-alpine3.16 AS builder

RUN apk update
RUN apk add git
RUN apk add ca-certificates;

WORKDIR /usr/src/app
COPY ./app .

ENV GO111MODULE=on
RUN go mod init inlab
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -ldflags="-s -w" -o bin/main ./first.go

### Executable Image
FROM alpine:3.16

COPY —from=builder /usr/src/app/bin/main ./main

EXPOSE 8001

ENTRYPOINT ["./main"]