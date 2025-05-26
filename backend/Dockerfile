FROM golang:1.17 AS builder

WORKDIR /app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

# Build the binary with static linking (to avoid dependency issues)
RUN CGO_ENABLED=0 GOOS=linux go build -o server ./cmd/api

FROM alpine:latest AS runner

COPY --from=builder /app/server /server

RUN addgroup -S backenduser && \
  adduser -S backenduser -G backenduser

RUN chown -R backenduser:backenduser /server
USER backenduser

EXPOSE 8081

CMD ["./server"]
