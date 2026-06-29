# Build stage
FROM golang:1.21-alpine AS builder

WORKDIR /app

# Download Go modules
COPY go.mod ./
RUN go mod download

# Copy source code and build a static binary
COPY . .
RUN CGO_ENABLED=0 go build -o user-service main.go

# Runtime stage — tiny final image
FROM alpine:3.19

WORKDIR /app
COPY --from=builder /app/user-service .

EXPOSE 8081
CMD ["./user-service"]