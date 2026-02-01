# Fixes Applied to Stable Diffusion WebUI Docker

This is a **working, fixed version** of the abandoned [stable-diffusion-webui-docker](https://github.com/AbdBarho/stable-diffusion-webui-docker) project.

## What Was Broken

The original project (7,327+ stars, 1,269+ forks) was abandoned in August 2024 with **68 critical open issues**. The most problematic:

### Issue #719 & #742: TypeIs Import Error (15+ reactions)
```
ImportError: cannot import name 'TypeIs' from 'typing_extensions'
```

**Impact:** Docker build completely failed. Users couldn't run Stable Diffusion.

**Root Cause:** The PyTorch base image (`pytorch/pytorch:2.3.0-cuda12.1-cudnn8-runtime`) shipped with `typing_extensions <4.6.0`, which doesn't include `TypeIs`.

## What We Fixed

### ✅ Fix #1: Upgraded typing_extensions

**Files Modified:**
- `services/AUTOMATIC1111/Dockerfile`
- `services/comfy/Dockerfile`

**Change:** Added `pip install --upgrade typing_extensions>=4.6.0` before dependency installation in both Dockerfiles.

**Result:** Build now succeeds. TypeIs import error eliminated.

## How to Use This Fixed Version

### Quick Start
```bash
git clone https://github.com/dmorsepgh/stable-diffusion-webui-docker.git
cd stable-diffusion-webui-docker
docker compose --profile auto up --build
```

### What Works Now
- ✅ AUTOMATIC1111 WebUI builds without errors
- ✅ ComfyUI builds without errors
- ✅ CPU and GPU profiles work
- ✅ All original features intact

## Why This Matters

**7,327 people starred this project** because it was the easiest way to run Stable Diffusion in Docker. Then it broke. Now it works again.

## Original Project Credits

Original work by [AbdBarho](https://github.com/AbdBarho). All credit for the base project goes to the original maintainers.

## Our Contribution

We found the abandoned project, diagnosed the issue, and fixed it so the community can use it again. That's what we do - rescue valuable abandoned open source projects.

---

**Fixed by:** Doug Morse
**Date:** February 2026
**Status:** Working and tested
