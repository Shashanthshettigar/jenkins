#!/bin/bash 

# Exit immediately if any command fails
set -e

# Update system packages
sudo yum update -y

# Install required utilities
sudo yum install -y wget git

# Install Java 17 (required for Jenkins)
sudo yum install -y java-17-amazon-corretto

# Verify Java installation
java -version

# Add Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo

# Import Jenkins GPG key
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

# Install Jenkins
sudo yum install -y jenkins

# Reload systemd to recognize Jenkins service
sudo systemctl daemon-reload

# Start Jenkins service
sudo systemctl start jenkins

# Enable Jenkins to start on boot
sudo systemctl enable jenkins

# Check Jenkins status
sudo systemctl status jenkins --no-pager
