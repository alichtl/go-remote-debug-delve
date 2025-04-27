FROM golang:1.24-alpine AS build
WORKDIR /
COPY . .
RUN CGO_ENABLED=0 go install github.com/go-delve/delve/cmd/dlv@latest
RUN CGO_ENABLED=0 go build -gcflags "all=-N -l" -o ./app

FROM scratch
COPY --from=build /go/bin/dlv /dlv
COPY --from=build /app /app
ENTRYPOINT [ "/dlv" ]
