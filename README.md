# Docker Compose Setup with NVIDIA GPU Support

This repository provides a Docker Compose configuration for running services with NVIDIA GPU acceleration.

## Prerequisites

- Docker Engine
- NVIDIA GPU with compatible drivers (version 550+)
- CUDA 12.4 and cuDNN 8
- NVIDIA Container Toolkit

## Installation Steps

1. **Install Docker Engine**
   - Follow the official installation guide: https://docs.docker.com/engine/install/

2. **Install NVIDIA Drivers and CUDA**
   - Ensure NVIDIA Drivers (550+) are installed
   - Install CUDA 12.4: https://developer.nvidia.com/cuda-12-4-0-download-archive
   - Install cuDNN 8: https://developer.nvidia.com/rdp/cudnn-archive

3. **Install NVIDIA Container Toolkit**
   - Follow the installation guide: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

4. **Setup Docker Compose**
   - Rename `docker-compose.example.yml` to `docker-compose.yml`

5. **Generate SSL Certificates**
   - See instructions below

6. **Start the Services**
   - Run `docker compose up -d --build`

## Generating SSL Certificates

### On Linux

```bash
# Generate a private key
openssl genrsa -out server.key 2048

# Generate a certificate signing request
openssl req -new -key server.key -out server.csr

# Generate a self-signed certificate
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

### On Windows with PuTTY

1. Generate SSL certificates using OpenSSL:
   - Install OpenSSL for Windows
   - Use the same commands as Linux above in Command Prompt or PowerShell

2. If you already have a PuTTY (.ppk) key and need to convert it:
   - Use PuTTYgen to load your .ppk file
   - Go to Conversions -> Export OpenSSH key
   - Save the exported key as `server.key`

## GPU Compatibility

Make sure your GPU supports CUDA 12.4 compute capability. Check the NVIDIA support matrix to confirm compatibility:
https://docs.nvidia.com/deeplearning/cudnn/backend/latest/reference/support-matrix.html

You may need to select a different CUDA version based on your GPU model.

## Usage

After following the installation steps and starting the services with `docker compose up -d`, you can access the application according to the configuration in your docker-compose.yml file.

## Troubleshooting

- If you encounter issues with NVIDIA GPU support, ensure the NVIDIA Container Toolkit is properly installed and configured
- Check docker logs with `docker compose logs` to diagnose issues

## Additional Resources

You can find a tutorial that goes a bit more in depth here: https://jaredweisinger.blog/setting-up-nextcloud-v30-fpm-with-nginx-and-cuda-cudnn8-for-the-recognize-app-on-ubuntu-24-04-605ffdcaba44

If you run into any problems, comment on that article and I will be happy to help.
