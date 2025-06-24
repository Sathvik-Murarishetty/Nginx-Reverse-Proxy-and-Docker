FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 go build -o /app/service1 ./main.go

FROM alpine:latest

WORKDIR /app
COPY --from=builder /app/service1 .

EXPOSE 8001

CMD ["/app/service1"]