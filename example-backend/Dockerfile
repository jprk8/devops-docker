FROM golang:1.26

WORKDIR /usr/src/app

COPY . .

ENV REQUEST_ORIGIN=http://localhost:8000
RUN go build && \
    go clean -cache -modcache && \
    rm -rf /go/pkg /root/.cache/go-build .git *.go go.mod go.sum && \
    useradd -m appuser

EXPOSE 8080

CMD ["./server"]
