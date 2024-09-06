# Use the RHEL 9 base image
FROM registry.access.redhat.com/ubi9/ubi

# Set the maintainer label (optional)
LABEL maintainer="your-email@example.com"

# Update the system and install necessary tools
RUN yum -y update && \
    yum -y install \
    vim \
    curl \
    wget \
    git \
    nano \
    python3 \
    python3-pip \
    && yum clean all

# Install Ansible using pip
RUN pip3 install ansible

# Install Terraform
RUN yum -y install dnf && \
    dnf -y install yum-utils && \
    yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo && \
    yum -y install terraform

# Set the working directory inside the container
WORKDIR /app

# Copy your application code (if any) to the container
# COPY ./your-app /app

# Example command (this can be whatever you want to run)
CMD ["/bin/bash"]
