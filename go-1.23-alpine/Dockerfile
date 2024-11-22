# Stage 1: Build the Go binary
FROM golang:1.23-alpine3.20 AS builder

# Set the current working directory inside the container
WORKDIR /go/src/app

# Copy the Go module files
COPY go.mod go.sum ./

# Download Go module dependencies
RUN go mod tidy

# Copy the source code into the container
COPY . .

# Build the Go binary
RUN go build -o myapp .

# Stage 2: Create the final image
FROM alpine:latest

# Install any required system dependencies (if needed, e.g., libc, ca-certificates)
RUN apk update && apk add --no-cache ca-certificates

# Copy the binary from the builder image
COPY --from=builder /go/src/app/myapp /usr/local/bin/myapp

# Set environment variables
ENV APP_ENV=production

# Set the default command to run your Go application
CMD ["/usr/local/bin/myapp"]
