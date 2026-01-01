FROM golang:1.25-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o metadata ./cmd/metadata

FROM alpine
WORKDIR /app
COPY --from=builder /app/metadata .
EXPOSE 50051

CMD ["./metadata"]
