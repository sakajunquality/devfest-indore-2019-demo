FROM golang:1.13-alpine as golang-base
FROM alpine as alpine-base

FROM golang-base as build
RUN apk add alpine-sdk
WORKDIR $GOPATH/src/github.com/sakajunquality/devfest-indore-2019-demo/app
COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

FROM alpine-base
RUN apk add --no-cache ca-certificates curl \
    && adduser -S me
COPY --from=build /go/bin/app /usr/local/bin/app

USER me

CMD ["app"]
EXPOSE 8080
