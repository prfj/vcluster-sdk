# Build the manager binary
FROM golang:1.22.2 as builder

# Make sure we use go modules
WORKDIR /vcluster

# Copy the Go Modules manifests
COPY . .

# Install dependencies
RUN go mod vendor && \
    CGO_ENABLED=0 GO111MODULE=on go build -mod vendor -o /plugin main.go

# we use alpine for easier debugging
FROM alpine:3.20.0

# Set root path as working directory
WORKDIR /

RUN mkdir -p /plugin

COPY --from=builder /plugin /plugin/plugin
