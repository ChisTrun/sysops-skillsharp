# Kế thừa từ image envoyproxy/ratelimit với tag cụ thể
FROM envoyproxy/ratelimit:master

# Thiết lập thư mục làm việc
WORKDIR /app

# Sao chép file cấu hình tùy chỉnh (đảm bảo config.yaml tồn tại cùng thư mục với Dockerfile)
COPY /config/config.yaml /app/config.yaml

# Cài đặt các phụ thuộc cần thiết (tùy chọn, để debug hoặc mở rộng)
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/* /

# Expose các cổng mặc định cho Envoy Rate Limit (8080 cho gRPC, 8081 cho HTTP)
EXPOSE 8080 8081
# Chạy Envoy Rate Limit với file cấu hình tùy chỉnh
CMD ["/usr/local/bin/ratelimit", "--config", "/app/config.yaml"]