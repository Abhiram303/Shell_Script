# Detects the OS & install the pkg or service:
**1. Displays the OS name.**

**2. Prompts the user for the service name to install.**

**3. Based on the OS, runs the correct installation commands.**

**4. Uses conditional steps for each OS type.**

```bash
#!/bin/bash

**# Detect OS**
if [ -f /etc/os-release ]; then
    . /etc/os-release
    OS=$ID
else
    echo "Unable to detect OS!"
    exit 1
fi

echo "Detected OS: $OS"

# Ask user for the service name
read -p "Enter the service name you want to install: " service

# Install based on OS
if [[ "$OS" == "ubuntu" || "$OS" == "debian" ]]; then
    echo "Updating package list..."
    sudo apt update -y
    echo "Installing $service on $OS..."
    sudo apt install -y "$service"

elif [[ "$OS" == "centos" || "$OS" == "rhel" ]]; then
    echo "Installing $service on $OS..."
    sudo yum install -y "$service"

elif [[ "$OS" == "rocky" ]]; then
    echo "Installing $service on $OS..."
    sudo dnf install -y "$service"

elif [[ "$OS" == "amzn" ]]; then
    echo "Installing $service on Amazon Linux..."
    sudo yum install -y "$service"

else
    echo "OS $OS not supported in this script!"
    exit 1
fi

# Verify installation
if command -v $service &> /dev/null; then
    echo "$service installed successfully!"
else
    echo "Installation failed or $service command not found!"
fi
```
