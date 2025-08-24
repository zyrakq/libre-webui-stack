# 🌐 Libre WebUI

A modular Docker Compose configuration system for Libre WebUI with support for multiple environments and extensions.

## 🏗️ Project Structure

```sh
src/libre-webui/
├── components/                              # Source compose components
│   ├── base/                               # Base components
│   │   ├── docker-compose.yml              # Main Libre WebUI service
│   │   └── .env.example                    # Base environment variables
│   ├── environments/                       # Environment components
│   │   ├── devcontainer/
│   │   │   └── docker-compose.yml          # DevContainer environment
│   │   ├── forwarding/
│   │   │   └── docker-compose.yml          # Port forwarding environment
│   │   ├── letsencrypt/
│   │   │   ├── docker-compose.yml          # Let's Encrypt SSL
│   │   │   └── .env.example                # Let's Encrypt variables
│   │   └── step-ca/
│   │       ├── docker-compose.yml          # Step CA SSL
│   │       └── .env.example                # Step CA variables
│   └── extensions/                         # Extension components
│       ├── openrouter/
│       │   ├── docker-compose.yml          # OpenRouter integration
│       │   └── .env.example                # OpenRouter variables
│       └── step-ca-trust/
│           ├── docker-compose.yml          # Step CA trust
│           └── .env.example                # Step CA trust variables
├── extensions.yml                          # Extension compatibility configuration
├── build/                        # Generated configurations (auto-generated)
│   ├── devcontainer/
│   │   ├── base/                           # DevContainer + base
│   │   ├── openrouter/                     # DevContainer + OpenRouter
│   │   ├── step-ca-trust/                  # DevContainer + Step CA trust
│   │   └── openrouter+step-ca-trust/       # DevContainer + OpenRouter + Step CA trust
│   ├── forwarding/
│   │   ├── base/                           # Forwarding + base
│   │   ├── openrouter/                     # Forwarding + OpenRouter
│   │   ├── step-ca-trust/                  # Forwarding + Step CA trust
│   │   └── openrouter+step-ca-trust/       # Forwarding + OpenRouter + Step CA trust
│   ├── letsencrypt/
│   │   ├── base/                           # Let's Encrypt + base
│   │   ├── openrouter/                     # Let's Encrypt + OpenRouter
│   │   ├── step-ca-trust/                  # Let's Encrypt + Step CA trust
│   │   └── openrouter+step-ca-trust/       # Let's Encrypt + OpenRouter + Step CA trust
│   └── step-ca/
│       ├── base/                           # Step CA + base
│       ├── openrouter/                     # Step CA + OpenRouter
│       ├── step-ca-trust/                  # Step CA + Step CA trust
│       └── openrouter+step-ca-trust/       # Step CA + OpenRouter + Step CA trust
├── build.sh                      # Build script
└── README.md                     # This file
```

## 🚀 Quick Start

### 1. Build Configurations

Run the build script to generate all possible combinations:

```bash
./build.sh
```

This will create all combinations in the `build/` directory.

### 2. Choose Your Configuration

Navigate to the desired configuration directory:

```bash
# For development with DevContainer
cd build/devcontainer/base/

# For development with port forwarding
cd build/forwarding/base/

# For production with Let's Encrypt SSL
cd build/letsencrypt/base/

# For production with Let's Encrypt + OpenRouter
cd build/letsencrypt/openrouter/

# For production with Step CA + OpenRouter + Step CA trust
cd build/step-ca/openrouter+step-ca-trust/

# For development with DevContainer + OpenRouter + Step CA trust
cd build/devcontainer/openrouter+step-ca-trust/
```

### 3. Configure Environment

Copy and edit the environment file:

```bash
cp .env.example .env
# Edit .env with your values
```

### 4. Deploy

Start the services:

```bash
docker-compose up -d
```

## 🔧 Available Configurations

### Environments

- **devcontainer**: Development environment with workspace network
- **forwarding**: Development environment with port forwarding
- **letsencrypt**: Production with Let's Encrypt SSL certificates
- **step-ca**: Production with Step CA SSL certificates

### Extensions

- **openrouter**: OpenRouter AI provider integration
- **step-ca-trust**: Step CA certificate trust integration

### Generated Combinations

#### Single Extensions

Each environment can be combined with any single extension:

- `devcontainer/base` - Basic development setup
- `devcontainer/openrouter` - Development with OpenRouter integration
- `devcontainer/step-ca-trust` - Development with Step CA certificate trust
- `forwarding/base` - Basic development with port forwarding
- `forwarding/openrouter` - Development with port forwarding + OpenRouter
- `forwarding/step-ca-trust` - Development with port forwarding + Step CA trust
- `letsencrypt/base` - Production with Let's Encrypt
- `letsencrypt/openrouter` - Production with Let's Encrypt + OpenRouter
- `letsencrypt/step-ca-trust` - Production with Let's Encrypt + Step CA trust
- `step-ca/base` - Production with Step CA
- `step-ca/openrouter` - Production with Step CA + OpenRouter
- `step-ca/step-ca-trust` - Production with Step CA + Step CA trust

#### Extension Combinations

When [`extensions.yml`](extensions.yml) is present, additional combinations are generated:

- `devcontainer/openrouter+step-ca-trust` - Development with OpenRouter + Step CA trust
- `forwarding/openrouter+step-ca-trust` - Development with port forwarding + OpenRouter + Step CA trust
- `letsencrypt/openrouter+step-ca-trust` - Production with Let's Encrypt + OpenRouter + Step CA trust
- `step-ca/openrouter+step-ca-trust` - Production with Step CA + OpenRouter + Step CA trust

## 🔧 Environment Variables

### Base Configuration

- `COMPOSE_PROJECT_NAME`: Project name for Docker Compose (default: libre-webui)
- `DOCKER_ENV`: Docker environment flag (default: true)
- `NODE_ENV`: Node.js environment (default: production)
- `VITE_API_TIMEOUT`: API timeout for Vite (default: 300000)
- `CORS_ORIGIN`: CORS origin URL (default: <http://localhost:5173>)
- `PORT`: Backend port (default: 3001)
- `FRONTEND_PORT`: Frontend port (default: 5173)
- `SINGLE_USER_MODE`: Enable single user mode (default: false)
- `JWT_EXPIRES_IN`: JWT token expiration (default: 7d)
- `JWT_SECRET`: JWT secret key
- `SESSION_SECRET`: Session secret key
- `ENCRYPTION_KEY`: Encryption key for sensitive data
- `OLLAMA_BASE_URL`: Ollama API base URL (default: <http://localhost:11434>)
- `OLLAMA_TIMEOUT`: Ollama API timeout (default: 300000)
- `OLLAMA_LONG_OPERATION_TIMEOUT`: Ollama long operation timeout (default: 900000)

### Let's Encrypt Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 5173)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### Step CA Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 5173)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### OpenRouter Configuration

- `OPENROUTER_API_KEY`: API key for OpenRouter service

### Step CA Trust Configuration

- `STEP_CA_TRUST`: Enable Step CA certificate trust (default: true)
- `STEP_CA_TRUST_RESTART`: Restart container when trust configuration changes (default: true)

The step-ca-trust extension automatically configures containers to trust certificates issued by Step CA, enabling secure communication with Step CA-protected services.

## 🔗 Extension Combinations

### Configuration File

Extension combinations are configured via [`extensions.yml`](extensions.yml). This file defines:

- **Groups**: Extensions that conflict with each other
- **Combinations**: Valid extension combinations to generate
- **Compatibility**: Rules for which extensions can work together

### Example Configuration

```yaml
# Extension compatibility configuration
version: "1.0"

# Extension groups - extensions in same group can be combined
groups:
  providers:
    description: "AI Providers"
    extensions:
      - openrouter

  step-ca:
    description: "smallstep-ca"
    extensions:
      - step-ca-trust

# Valid combinations
combinations:
  - name: "openrouter+step-ca-trust"
    extensions: ["openrouter", "step-ca-trust"]
    description: "OpenRouter with Step CA trust"
```

### Backward Compatibility

- **Without `extensions.yml`**: Only single extensions are generated (legacy behavior)
- **With `extensions.yml`**: Both single extensions and combinations are generated
- **Existing configurations**: Remain unchanged and fully compatible

## ⚠️ Known Issues

### AI Providers

- **OpenRouter**: May not work correctly with current configuration
- **Other providers**: Possible compatibility issues with some external AI providers

It is recommended to thoroughly test integration with external providers before using in production.

## 🛠️ Development

### Adding New Components

1. **New Environment**: Create directory in `components/environments/` with `docker-compose.yml` and optional `.env.example` file
2. **New Extension**: Create directory in `components/extensions/` with `docker-compose.yml` and optional `.env.example` file
3. **Update Combinations**: Add new extension to [`extensions.yml`](extensions.yml) if it should be part of combinations
4. **Rebuild**: Run `./build.sh` to generate new combinations

### Adding Extension Combinations

1. **Edit Configuration**: Modify [`extensions.yml`](extensions.yml)
2. **Define Groups**: Add extensions to appropriate groups
3. **Add Combinations**: Specify valid extension combinations
4. **Rebuild**: Run `./build.sh` to generate new combinations

### Modifying Existing Components

1. Edit the component files in `components/`
2. Run `./build.sh` to regenerate configurations
3. The `build/` directory will be completely recreated

## 📝 Notes

- The `build/` directory is automatically generated and should not be edited manually
- Extension combinations are only generated when [`extensions.yml`](extensions.yml) exists
- User `.env` files are preserved during rebuilds
