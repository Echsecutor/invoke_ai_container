[![Building Container](https://github.com/Echsecutor/invoke_ai_container/actions/workflows/build-all.yml/badge.svg)](https://github.com/Echsecutor/invoke_ai_container/actions/workflows/build-all.yml)

# Shipping Invoke AI

<img alt="Artificial Inteligence Cyborg Shipping" src="./shipping_ai.png" height="500" />

This is a minimalist container running invoke web UI 5.5.0. No nonsense included. Just starts the invoke web ui and exposes the port.

- [You can run this image on runpod](https://runpod.io/console/deploy?template=elr3w646vn&ref=c71blwtm)
- See https://www.invoke.com/ for Invoke AI Details
  - This container is not created by/endorsed by invoke.
  - I have just turned the installation manual at https://invoke-ai.github.io/InvokeAI/installation/manual/#walkthrough into a Dockerfile.

## Working Invoke AI Features (testet in container on runpod)
- Install + Use starter Models/Models from Huggin Face/Any Models via URL, e.g. from civitai
- Benchmarks on runpod on A40:
  - SD1,
    - Image generation wall clock time (512x512, 30 steps)  <3s
  - SDXL/Pony
    - Image generation wall clock time (1024x1024, 30 steps) <10s
  - FLUX Models
    - Image generation wall clock time (1024x1024, 30 step) <30s

## Config
- Models are stored in the volume mounted under `/workspace`
- Outputs (Images) are stored in the container under `/invoke/outputs`
- Invoke AI Web Service exposed on port 8080 (no login)
- Exposes Port 22 for scp (through runpod forwarding)


# Scripts

- This repository contains [a script](./install_invoke_ai.sh) version of the manual found at 
https://invoke-ai.github.io/InvokeAI/installation/manual/
to install invoke ai into a fresh ubuntu image.

- This script [is applied to create a container image](./Dockerfile).

## Usage

Run locally:
- Be sure to have nvidia stuff installed: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

```
docker run --gpus device=0 --rm -it --name invoke -p 8080:8080 -v YOUR_LOCAL_MODEL_DIR:/workspace ghcr.io/echsecutor/invoke_ai_container:latest
```

# License

Copyright 2025 Sebastian Schmittner

<a href="https://opensource.org/license/mit">
<img alt="Open Source Initiative Approved License" height="200" src="https://opensource.org/wp-content/themes/osi/assets/img/osi-badge-light.svg" />
</a>

All code in this repository is distributed under the <a href="./LICENSE">MIT License</a>.
