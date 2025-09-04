# Libre WebUI Custom Image

Custom Docker image for Libre WebUI with dynamic configuration generation based on environment variables.

## Quick Start

Build the custom Libre WebUI image:

```bash
cd src/libre-webui/image
docker build -t libre-webui .
docker tag libre-webui localhost/libre-webui
```
