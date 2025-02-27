# Use the official Golang image as a builder
FROM golang:1.21 as builder

# Set working directory
FROM golang:1.21-alpine AS build

WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy source code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o auth-api .

# Final stage
FROM alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

# Copy the binary from the build stage
COPY --from=build /app/auth-api .

# Expose port
EXPOSE 8081

# Command to run
CMD ["./auth-api"]