FROM golang:1.13 as builder
WORKDIR /app
COPY . ./

# Print the Go version and environment variables
RUN go version
RUN go env

# Clean the Go module cache and tidy up dependencies
RUN go clean -modcache
RUN go mod tidy

# List the contents of the current directory to verify files
RUN ls -al

# Build the Go application with verbose output to help identify issues
RUN CGO_ENABLED=0 GOOS=linux go build -v -o server .

FROM alpine:3
RUN apk add --no-cache ca-certificates
COPY --from=builder /app/server /
CMD ["/server"]
