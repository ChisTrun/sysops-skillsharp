# Kế thừa từ image envoyproxy/ratelimit với tag cụ thể
FROM envoyproxy/ratelimit:master

# Thiết lập thư mục làm việc
WORKDIR /app

# Sao chép file cấu hình tùy chỉnh (đảm bảo config.yaml tồn tại cùng thư mục với Dockerfile)
COPY /config/config.yaml /app/config.yaml

RUN if [ -f /etc/alpine-release ]; then \
    apk update && apk add --no-cache curl; \
    fi

# Expose các cổng mặc định cho Envoy Rate Limit (8080 cho gRPC, 8081 cho HTTP)
EXPOSE 8080 8081
# Chạy Envoy Rate Limit với file cấu hình tùy chỉnh
CMD ["/usr/local/bin/ratelimit", "--config", "/app/config.yaml"]