# Use official NGINX image as base
FROM nginx:latest

# Install dependencies for compiling NGINX with RTMP module
RUN apt-get update && \
    apt-get install -y \
    libpcre3 \
    libpcre3-dev \
    libssl-dev \
    zlib1g-dev \
    git \
    build-essential

# Clone the RTMP module from GitHub
RUN git clone https://github.com/arut/nginx-rtmp-module.git /usr/local/src/nginx-rtmp-module

# Download and compile NGINX with RTMP module
RUN wget https://nginx.org/download/nginx-1.21.0.tar.gz && \
    tar -zxvf nginx-1.21.0.tar.gz && \
    cd nginx-1.21.0 && \
    ./configure --add-module=/usr/local/src/nginx-rtmp-module && \
    make && \
    make install

# Copy custom nginx.conf to enable RTMP module configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose the default HTTP and RTMP ports
EXPOSE 80 1935

# Start NGINX in the foreground
CMD ["nginx", "-g", "daemon off;"]

