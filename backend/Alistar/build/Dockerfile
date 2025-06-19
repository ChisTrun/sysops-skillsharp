FROM envoyproxy/ratelimit:master

# Copy thư mục config chứa file config.yaml vào image
COPY config /data

# Thiết lập biến môi trường cho rate limit service
ENV RUNTIME_ROOT=/data
ENV RUNTIME_SUBDIRECTORY=.
ENV LOG_LEVEL=debug
