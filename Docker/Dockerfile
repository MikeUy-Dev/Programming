# Use the RHEL 9 base image
FROM registry.access.redhat.com/ubi9/ubi:latest

# Install necessary packages for Ansible, Terraform, and SSH
RUN yum update -y --allowerasing && \
    yum install -y --allowerasing \
    openssh-server \
    openssh-clients \
    sudo \
    curl \
    unzip \
    tar \
    && yum clean all

# Install Terraform
RUN curl -fsSL https://releases.hashicorp.com/terraform/1.5.7/terraform_1.5.7_linux_amd64.zip -o terraform.zip && \
    unzip terraform.zip && \
    mv terraform /usr/local/bin/ && \
    rm -f terraform.zip

# Create Ansible user with passwordless sudo
RUN useradd -m -s /bin/bash ansible && \
    echo 'ansible ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set up SSH for the ansible user
RUN mkdir -p /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    chown -R ansible:ansible /home/ansible/.ssh

# Add SSH key to authorized_keys (optional, replace with your public key)
COPY id_rsa.pub /home/ansible/.ssh/authorized_keys
RUN chmod 600 /home/ansible/.ssh/authorized_keys && \
    chown ansible:ansible /home/ansible/.ssh/authorized_keys

# Expose SSH port
EXPOSE 22

# Start SSH service
RUN ssh-keygen -A
CMD ["/usr/sbin/sshd", "-D"]

