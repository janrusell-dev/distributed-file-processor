FROM golang:1.25-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o result ./cmd/result

FROM alpine
WORKDIR /app
COPY --from=builder /app/result .
EXPOSE 50051

CMD ["./result"]
