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

# Set authorized SSH keys
RUN touch /home/git/.ssh/authorized_keys \
    && chown git:git /home/git/.ssh/authorized_keys \
    && chmod 600 /home/git/.ssh/authorized_keys

# Generate host keys
RUN ssh-keygen -A

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
