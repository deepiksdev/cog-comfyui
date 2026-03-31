# cog-comfyui

Run ComfyUI workflows on Replicate using Cog.

## Running on Mac (No GPU Required)

It is entirely possible to develop, build, and deploy Cog models on a Mac without a dedicated GPU. Cog is designed to work seamlessly on **macOS** and **Linux**, primarily leveraging **Docker** to create and manage its environments.

### 1. The Build Phase (No GPU Needed)
You can build your Cog image (the "suitcase" that packages your code) entirely on your Mac's CPU. Cog bundles your Python code, custom nodes, and the ComfyUI engine into a portable Docker image.

> [!IMPORTANT]
> You must have [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/) installed and running, as Cog relies on it to package everything.

### 2. Testing Locally (Running on CPU)
You can test your model locally using your Mac's CPU:
* **Default Behavior:** If you don't specify `gpu: true` in your `cog.yaml`, the environment will run using the CPU.
* **Auto-Fallback:** If your `predict.py` or ComfyUI nodes are written to use PyTorch, they will automatically fall back to CPU mode if they don't detect a GPU. Note that while functional, this will be significantly slower for image generation tasks.

### 3. Deploying to Replicate
The most important advantage is that **your local hardware doesn't limit where the model runs.** Even if you build on a GPU-less Mac, once you run `cog push`, your model is uploaded to Replicate's high-performance servers. When you or your users trigger a prediction via the API, Replicate runs that code on **high-end NVIDIA GPUs** in the cloud.

---

## Requirements for Mac
To get started on your Mac, you only need:
* **Homebrew:** To install Cog easily (`brew install replicate/tap/cog`).
* **Docker Desktop:** Must be running in the background.
* **macOS:** 10.15 or later (supports Intel and Apple Silicon).

## Summary of the "No GPU" Workflow
1. **Develop:** Write your nodes and JSON workflows on your Mac.
2. **Package:** Run `cog build` (this uses your Mac's CPU and Docker).
3. **Push:** Run `cog push` to send it to Replicate.
4. **Run:** Execute the workflow on Replicate's cloud GPUs, controlled from your Mac.

Since your goal is to get your custom nodes onto Replicate, your Mac is perfectly capable of doing the "packing" and "uploading" parts of the job.
