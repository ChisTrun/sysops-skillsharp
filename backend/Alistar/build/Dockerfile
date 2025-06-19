# Giai đoạn 1: Build binary từ mã nguồn
FROM golang:1.21-alpine AS builder

# Cài đặt các công cụ cần thiết
RUN apk add --no-cache git

# Thiết lập thư mục làm việc
WORKDIR /app

# Clone mã nguồn envoyproxy/ratelimit
RUN git clone https://github.com/envoyproxy/ratelimit.git .

# Build binary
RUN go mod tidy && \
    go build -o ratelimit ./cmd/ratelimit

# Giai đoạn 2: Tạo image nhẹ để chạy
FROM alpine:3.18

# Cài đặt các phụ thuộc runtime
RUN apk add --no-cache ca-certificates

# Copy binary từ giai đoạn builder
COPY --from=builder /app/ratelimit /usr/local/bin/ratelimit

# Tạo thư mục cho cấu hình
RUN mkdir /config

# Copy tệp cấu hình từ thư mục config
COPY config/config.yaml /config/ratelimit-config.yaml

# Đặt biến môi trường cho Redis (có thể override qua Helm hoặc Kubernetes)
ENV REDIS_AUTH=Skillsharp@123

# Expose cổng mặc định của ratelimit
EXPOSE 8081

# Lệnh chạy dịch vụ
CMD ["/usr/local/bin/ratelimit", "-config=/config/ratelimit-config.yaml"]