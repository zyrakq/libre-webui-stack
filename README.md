# 🐳 Libre WebUI Docker Stack

This project contains a collection of Docker configurations and compose files for running Libre WebUI and related services.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](src/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](src/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](src/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](src/ssl-automation/step-ca-manager/README.md).

## 🌐 Services

### [🌐 Libre WebUI](src/libre-webui)

Libre WebUI — the main service providing a user interface for AI interactions with modular Docker Compose configuration system supporting multiple environments and extensions.
[Learn more about Libre WebUI configuration](src/libre-webui/README.md).

### [🤖 Ollama](src/ollama)

Ollama AI service — modular Docker Compose configuration system supporting multiple environments and extensions with GPU acceleration support.
[Learn more about Ollama configuration](src/ollama/README.md).

## 🚀 Getting Started

To run the services, use the appropriate `docker-compose.yml` files in the subprojects. Make sure all environment variables are configured correctly.

Each service directory contains:

- 📋 Docker Compose configurations
- 🔧 Environment variable examples
- 📖 Detailed setup instructions
- 🛠️ Helper scripts for development and production

## 🏗️ Project Structure

```sh
├── src/
│   ├── ssl-automation/      # SSL certificate automation
│   │   ├── letsencrypt-manager/ # Let's Encrypt SSL certificate management
│   │   └── step-ca-manager/     # Local CA and trusted certificates
│   ├── libre-webui/         # Main Libre WebUI service configs
│   │   ├── components/      # Modular compose components
│   │   │   ├── base/        # Base Libre WebUI service
│   │   │   ├── environments/ # Environment configurations
│   │   │   └── extensions/  # Extension configurations
│   │   └── build/           # Generated configurations (auto-generated)
│   └── ollama/              # Ollama AI service configs
│       ├── components/      # Modular compose components
│       │   ├── base/        # Base Ollama service
│       │   ├── environments/ # Environment configurations
│       │   └── extensions/  # Extension configurations
│       └── build/           # Generated configurations (auto-generated)
```

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)
