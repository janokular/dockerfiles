FROM alpine:3.24

# Install Bash shell OpenSSH and Git
RUN apk add --no-cache bash openssh git

# SSH configuration
RUN mkdir -p /var/run/sshd \
    && sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

# Create git user and repos directory
RUN adduser -D -s /bin/bash git \
    && passwd -u git \
    && mkdir -p /home/git/repos /home/git/.ssh/ \
    && chown -R git:git /home/git/ \
    && chmod 700 /home/git/.ssh \
    && chmod 700 /home/git/repos

# Create authorized_keys file and generate SSH host keys
RUN touch /home/git/.ssh/authorized_keys \
    && chown git:git /home/git/.ssh/authorized_keys \
    && chmod 600 /home/git/.ssh/authorized_keys \
    && ssh-keygen -A

# checkov:skip-CKV_DOCKER_1:SSH is the primary service of this Git server
EXPOSE 22

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
    CMD ["pgrep", "sshd"]

# checkov:skip=CKV_DOCKER_3:sshd requires root privileges
CMD ["/usr/sbin/sshd", "-D"]
