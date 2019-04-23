FROM golang:1.11.1-alpine as builder
WORKDIR /go/src/github.com/yardstick/restic
COPY . .
RUN go run build.go


FROM alpine:latest

COPY --from=builder /go/src/github.com/yardstick/restic/restic /usr/bin

RUN apk add --update --no-cache ca-certificates fuse openssh-client

ENTRYPOINT ["/usr/bin/restic"]
