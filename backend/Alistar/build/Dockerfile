# Giai đoạn 1: Build binary từ mã nguồn
FROM golang:1.21-alpine AS builder

# Cài đặt các công cụ cần thiết (bao gồm protoc nếu cần)
RUN apk add --no-cache git protoc

# Thiết lập thư mục làm việc
WORKDIR /app

# Clone mã nguồn envoyproxy/ratelimit (checkout tag cụ thể để tránh lỗi phiên bản)
RUN git clone https://github.com/envoyproxy/ratelimit.git . && \
    git checkout v1.5.0  # Checkout một phiên bản ổn định

# Khởi tạo và tải module
RUN go mod tidy

# Build binary
RUN go build -o ratelimit ./cmd/ratelimit

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

# Expose cổng mặc định của ratelimit
EXPOSE 8081

# Lệnh chạy dịch vụ, sử dụng biến môi trường từ bên ngoài
CMD ["/usr/local/bin/ratelimit", "-config=/config/ratelimit-config.yaml"]