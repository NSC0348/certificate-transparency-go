FROM golang:1.22.2-bookworm@sha256:b03f3ba515751657c75475b20941fef47341fccb3341c3c0b64283ff15d3fb46 as builder

ARG GOFLAGS=""
ENV GOFLAGS=$GOFLAGS

# Move to working directory /build
WORKDIR /build

# Copy and download dependency using go mod
COPY go.mod .
COPY go.sum .
RUN go mod download

# Copy the code into the container
COPY . .

# Build the application
RUN go build -o /build/bin/feeder ./internal/witness/cmd/feeder

# Build release image
FROM alpine@sha256:c5b1261d6d3e43071626931fc004f70149baeba2c8ec672bd4f27761f8e1ad6b

COPY --from=builder /build/bin/feeder /bin/feeder
ENTRYPOINT ["/bin/feeder"]
