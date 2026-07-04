# Jetson Orin Wheels

Pre-built Python wheels for NVIDIA Jetson Orin devices on ARM64 / aarch64.

中文说明请见 [README.zh-CN.md](README.zh-CN.md).

## Releases

Download wheels from the GitHub Releases page:

https://github.com/Shattered217/Jetson-Orin-Wheels/releases

Do not mix wheels across JetPack or Python versions. The `cp310` wheels are for Python 3.10, and the `cp312` wheels are for Python 3.12.

Make sure `uv` is already installed. See the official installation guide: https://docs.astral.sh/uv/getting-started/installation/

## Verified Environments

| Field | JetPack 7.2.0 | JetPack 6.2.1 rc1 |
| --- | --- | --- |
| Host used for verification | `Jetson-Orin-NX` | `Jetson-Orin-Nano` |
| Device | NVIDIA Jetson Orin NX Engineering Reference Developer Kit | NVIDIA Jetson Orin Nano Engineering Reference Developer Kit Super |
| OS | Ubuntu 24.04.4 LTS | Ubuntu 22.04.5 LTS |
| Jetson Linux / L4T | R39 revision 2.0 / `nvidia-l4t-core 39.2.0` | R36 revision 4.7 / `nvidia-l4t-core 36.4.7` |
| CUDA Toolkit | 13.2.1 | 12.6.11 |
| cuDNN | 9.20.0.46 for CUDA 13 | 9.3.0.75 for CUDA 12 |
| Python | 3.12.3 | 3.10.12 |
| System TensorRT | 10.16.2.10 | 10.3.0 |
| System OpenCV | 5.0.0 | 4.11.0 |

## JetPack 7.2.0

Release: https://github.com/Shattered217/Jetson-Orin-Wheels/releases/tag/7.2.0

### Package Matrix

| Package | Source | Version | Notes |
| --- | --- | --- | --- |
| PyTorch | [`torch-2.12.0-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torch-2.12.0-cp312-cp312-linux_aarch64.whl) | 2.12.0 | Python 3.12 / aarch64 wheel. |
| TorchVision | [`torchvision-0.27.0+78839c2-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torchvision-0.27.0%2B78839c2-cp312-cp312-linux_aarch64.whl) | 0.27.0 | Matches the PyTorch wheel above. |
| ONNX Runtime GPU | [`onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl) | 1.28.0 | Keep `numpy<2` pinned. |
| TensorRT | System Python package | 10.16.2.10 | Reuse through `--system-site-packages`. |
| OpenCV | System Python package | 5.0.0 | Reuse through `--system-site-packages`. |

### Create Environment

JetPack 7 reuses the system TensorRT and OpenCV packages through `--system-site-packages`.

```bash
uv venv .venv --python 3.12 --system-site-packages
source .venv/bin/activate
```

### Install Wheels

Install the JP7 wheels:

```bash
uv pip install \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torch-2.12.0-cp312-cp312-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torchvision-0.27.0%2B78839c2-cp312-cp312-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl" \
  "numpy<2"
```

### Verify

```bash
python - <<'PY'
import torch
import torchvision
import onnxruntime as ort
import tensorrt as trt
import cv2

print("torch:", torch.__version__)
print("torch cuda:", torch.cuda.is_available())
print("torchvision:", torchvision.__version__)
print("onnxruntime providers:", ort.get_available_providers())
print("tensorrt:", trt.__version__)
print("opencv:", cv2.__version__)
print("opencv cuda devices:", cv2.cuda.getCudaEnabledDeviceCount())
PY
```

## JetPack 6.x

Release: https://github.com/Shattered217/Jetson-Orin-Wheels/releases/tag/6.2.1rc1

These wheels were verified on JetPack 6.2.1 rc1. Compatibility across other JetPack 6.x minor versions is not guaranteed.

### Package Matrix

| Package | Source | Version | Notes |
| --- | --- | --- | --- |
| PyTorch | [`torch-2.3.0a0+git97ff6cf-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torch-2.3.0a0%2Bgit97ff6cf-cp310-cp310-linux_aarch64.whl) | 2.3.0a0 | Python 3.10 / aarch64 wheel. |
| TorchVision | [`torchvision-0.18.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchvision-0.18.0-cp310-cp310-linux_aarch64.whl) | 0.18.0 | Matches the PyTorch wheel above. |
| Torchaudio | [`torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl) | 0.18.0 | Minimal Jetson build. |
| ONNX Runtime GPU | [`onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl) | 1.24.0 | CUDA / TensorRT-enabled GPU build. |
| TensorRT | System Python package | 10.3.0 | Reuse through `--system-site-packages`. |
| OpenCV | System Python package | 4.11.0 | Reuse through `--system-site-packages`. |

### Create Environment

For JetPack 6, using `--system-site-packages` to reuse the system TensorRT and OpenCV packages is recommended first. If you prefer a fully wheel-based setup, you can manually install the TensorRT and OpenCV wheels from the release page.

```bash
uv venv .venv --python 3.10 --system-site-packages
source .venv/bin/activate
```

### Install Wheels

Install the JP6 wheels:

```bash
uv pip install \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torch-2.3.0a0%2Bgit97ff6cf-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchvision-0.18.0-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl" \
  "numpy<2"
```

### Verify

```bash
python - <<'PY'
import torch
import torchvision
import torchaudio
import onnxruntime as ort
import tensorrt as trt
import cv2

print("torch:", torch.__version__)
print("torch cuda:", torch.cuda.is_available())
print("torchvision:", torchvision.__version__)
print("torchaudio:", torchaudio.__version__)
print("onnxruntime providers:", ort.get_available_providers())
print("tensorrt:", trt.__version__)
print("opencv:", cv2.__version__)
print("opencv cuda devices:", cv2.cuda.getCudaEnabledDeviceCount())
PY
```

## YOLO Smoke Test

After installing PyTorch and OpenCV, Ultralytics YOLO can be checked with:

```bash
uv pip install ultralytics
yolo check
```

The output should show the Jetson GPU, CUDA availability, PyTorch, TorchVision, NumPy, and OpenCV versions.

## Troubleshooting

- **Wrong Python ABI**: `cp310` wheels require Python 3.10; `cp312` wheels require Python 3.12.
- **Wrong JetPack line**: Install wheels from the release tag matching your JetPack version.
- **NumPy compatibility**: Keep `numpy<2` pinned when using the ONNX Runtime GPU wheels.
- **TensorRT / OpenCV imports fail**: Recreate the environment with `--system-site-packages`.
- **Multiple Python environments**: Run `which python`, `python --version`, and `python -m pip --version` before installing.

## References

- [Jetson Orin Wheels releases](https://github.com/Shattered217/Jetson-Orin-Wheels/releases)
- [Jetson Python environment: reuse system packages with uv `--system-site-packages`](https://nvcc-v.com/2026/06/09/jetson-python-uv-system-site-packages/)
- [PyTorch for Jetson](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048)
- [TensorRT Python package source](https://github.com/NVIDIA/TensorRT/tree/release/10.3/python)
