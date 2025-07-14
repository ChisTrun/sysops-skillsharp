FROM envoyproxy/ratelimit:master

RUN mkdir -p /data/ratelimit/config

# Copy toàn bộ config từ thư mục host vào image
COPY ./config /data/ratelimit/config

# Biến môi trường cần thiết
ENV LOG_LEVEL=debug \
    REDIS_SOCKET_TYPE=tcp \
    REDIS_URL=redis://:Skillsharp%40123@10.128.0.3:6379 \
    RUNTIME_ROOT=/data \
    RUNTIME_SUBDIRECTORY=ratelimit \
    RUNTIME_WATCH_ROOT=false \
    CONFIG_TYPE=FILE 

CMD ["/bin/ratelimit"]
