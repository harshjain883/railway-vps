FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive

# Update aur zaroori tools install karein
RUN apt update && apt upgrade -y && \
    apt install -y \
    openssh-server \
    curl \
    wget \
    git \
    nano \
    sudo \
    python3 \
    python3-pip && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /run/sshd

# SSH Server Configuration (Authentication Fixes)
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && \
    echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config && \
    echo "KbdInteractiveAuthentication yes" >> /etc/ssh/sshd_config && \
    echo "UsePAM no" >> /etc/ssh/sshd_config

# Startup Script
RUN cat > /start.sh << 'EOF'
#!/bin/bash

# Fixed Password set karein
PASSWORD="${SSH_PASSWORD:-MySecretPass@123}"
echo "root:$PASSWORD" | chpasswd

# Railway TCP Proxy host aur port fetch karein
# Agar proxy add ho chuki hai toh auto-detect karega, nahi toh default value lega
HOST="${RAILWAY_TCP_PROXY_DOMAIN:-hayabusa.proxy.rlwy.net}"
PORT="${RAILWAY_TCP_PROXY_PORT:-20067}"

echo ""
echo "========================================"
echo "         SSH ACCESS DETAILS"
echo "========================================"
echo "Host        : $HOST"
echo "Port        : $PORT"
echo "Username    : root"
echo "Password    : $PASSWORD"
echo "SSH Command : ssh root@$HOST -p $PORT"
echo "========================================"
echo ""

# SSH daemon ko foreground me run karein
exec /usr/sbin/sshd -D
EOF

RUN chmod +x /start.sh

EXPOSE 22

CMD ["/bin/bash", "/start.sh"]
