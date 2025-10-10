FROM postgres:latest

# Set environment variables
ENV POSTGRES_USER=root
ENV POSTGRES_PASSWORD=root

# Use apt for Debian-based postgres image
RUN apt-get update && \
    apt-get install -y libzstd1 liblz4-1 && \
    apt-get install -y postgis && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 5432
