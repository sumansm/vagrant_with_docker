# Vagrant with Docker

A simple Vagrant configuration that sets up an Ubuntu VM with Docker pre-installed and configured.

**Author:** Suman Mondal  
**Repository:** https://github.com/sumansm/vagrant_with_docker

## Overview

This project provides a ready-to-use Vagrant configuration that automatically provisions an Ubuntu 22.04 (Jammy) virtual machine with Docker installed. It's perfect for developers who want a consistent, isolated environment for containerized applications.

## Features

- **Ubuntu 22.04 LTS (Jammy)** - Latest stable Ubuntu release
- **Docker CE** - Latest Docker Community Edition pre-installed
- **4GB RAM** - Sufficient memory for development workloads
- **Private Network** - Isolated network configuration (192.168.62.101)
- **Custom Hostname** - Easy identification (sumanvm-V4)
- **Automated Provisioning** - Zero-configuration Docker setup

## Prerequisites

Before using this project, ensure you have the following installed on your host machine:

- **VirtualBox** (6.1 or later)
- **Vagrant** (2.2 or later)

### Installation Links

- [VirtualBox Download](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant Download](https://www.vagrantup.com/downloads)

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sumansm/vagrant_with_docker.git
   cd vagrant_with_docker
   ```

2. **Start the VM:**
   ```bash
   vagrant up
   ```

3. **SSH into the VM:**
   ```bash
   vagrant ssh
   ```

4. **Verify Docker installation:**
   ```bash
   docker --version
   docker run hello-world
   ```

## Configuration Details

### VM Specifications
- **OS:** Ubuntu 22.04 LTS (Jammy)
- **RAM:** 4GB
- **Network:** Private network with IP 192.168.62.101
- **Hostname:** sumanvm-V4
- **Provider:** VirtualBox

### Installed Software
- Docker CE (latest stable version)
- Docker GPG key verification
- Custom DNS configuration (8.8.8.8)

## Usage Examples

### Basic Docker Commands
```bash
# Check Docker status
sudo systemctl status docker

# Run a simple container
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# Access from host machine
curl http://192.168.62.101:8080
```

### Development Workflow
```bash
# SSH into the VM
vagrant ssh

# Navigate to shared folder (if configured)
cd /vagrant

# Run your containerized application
docker-compose up -d
```

## Common Commands

### Vagrant Commands
```bash
# Start the VM
vagrant up

# Stop the VM
vagrant halt

# Restart the VM
vagrant reload

# Destroy the VM
vagrant destroy

# SSH into the VM
vagrant ssh

# Check VM status
vagrant status

# Re-run provisioning
vagrant provision
```

### Docker Commands (Inside VM)
```bash
# Basic Docker commands
docker --version
docker info
docker images
docker ps -a

# Container management
docker run -it ubuntu:latest /bin/bash
docker stop <container_id>
docker rm <container_id>

# Image management
docker pull <image_name>
docker rmi <image_id>
```

## Network Configuration

The VM is configured with:
- **Private Network IP:** 192.168.62.101
- **DNS:** 8.8.8.8 (Google DNS)
- **Host Access:** Services running in containers can be accessed from the host machine using the VM's IP

## Customization

### Modify VM Resources
Edit the `Vagrantfile` to change VM specifications:

```ruby
vb.memory = "2048"  # Change RAM allocation
vb.cpus = 2         # Add CPU configuration
```

### Change Network Settings
```ruby
sumanvm.vm.network "private_network", ip: "192.168.62.102"  # Change IP
```

### Add Additional Software
Add to the provisioning script in `Vagrantfile`:
```ruby
sumanvm.vm.provision "shell", inline: <<-SHELL
  # Existing Docker installation commands...
  
  # Add your custom software installation here
  sudo apt-get install -y git curl wget
SHELL
```

## Troubleshooting

### Common Issues

**1. VM fails to start:**
```bash
# Check VirtualBox installation
VBoxManage --version

# Verify Vagrant installation
vagrant --version

# Check for conflicting VMs
vagrant global-status
```

**2. Docker not accessible:**
```bash
# Check Docker service
sudo systemctl status docker

# Restart Docker service
sudo systemctl restart docker

# Add user to docker group
sudo usermod -aG docker $USER
```

**3. Network connectivity issues:**
```bash
# Check VM network configuration
ip addr show

# Test connectivity
ping 8.8.8.8

# Check routing
route -n
```

**4. Performance issues:**
```bash
# Increase VM memory in Vagrantfile
vb.memory = "6144"  # 6GB RAM

# Enable VT-x/AMD-V in BIOS
# Check with: grep -E "(vmx|svm)" /proc/cpuinfo
```

### Getting Help

- **Vagrant Documentation:** https://www.vagrantup.com/docs
- **Docker Documentation:** https://docs.docker.com
- **VirtualBox Documentation:** https://www.virtualbox.org/manual
- **Ubuntu Documentation:** https://ubuntu.com/server/docs

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

If you encounter any issues or have questions, please:
1. Check the [Troubleshooting](#troubleshooting) section
2. Search existing [Issues](https://github.com/sumansm/vagrant_with_docker/issues)
3. Create a new issue with detailed information

## Acknowledgments

- Ubuntu team for the excellent base image
- Docker team for the containerization platform
- Vagrant team for the development environment tool
- VirtualBox team for the virtualization platform

---

**Happy Coding!** 🚀