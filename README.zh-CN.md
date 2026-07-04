# Jetson Orin Wheels

面向 NVIDIA Jetson Orin 设备（ARM64 / aarch64）的预编译 Python wheels。

English version: [README.md](README.md).

## Releases

所有 wheel 均可从 GitHub Releases 下载：

https://github.com/Shattered217/Jetson-Orin-Wheels/releases

请不要跨 JetPack 或 Python 版本混用 wheels。`cp310` 对应 Python 3.10，`cp312` 对应 Python 3.12。

请确保已安装 `uv` 环境。安装方式见 uv 官方文档：https://docs.astral.sh/uv/getting-started/installation/

## 实测环境

| 字段 | JetPack 7.2.0 | JetPack 6.2.1 rc1 |
| --- | --- | --- |
| 验证主机 | `Jetson-Orin-NX` | `Jetson-Orin-Nano` |
| 设备 | NVIDIA Jetson Orin NX Engineering Reference Developer Kit | NVIDIA Jetson Orin Nano Engineering Reference Developer Kit Super |
| OS | Ubuntu 24.04.4 LTS | Ubuntu 22.04.5 LTS |
| Jetson Linux / L4T | R39 revision 2.0 / `nvidia-l4t-core 39.2.0` | R36 revision 4.7 / `nvidia-l4t-core 36.4.7` |
| CUDA Toolkit | 13.2.1 | 12.6.11 |
| cuDNN | 9.20.0.46 for CUDA 13 | 9.3.0.75 for CUDA 12 |
| Python | 3.12.3 | 3.10.12 |
| 系统 TensorRT | 10.16.2.10 | 10.3.0 |
| 系统 OpenCV | 5.0.0 | 4.11.0 |

## JetPack 7.2.0

Release: https://github.com/Shattered217/Jetson-Orin-Wheels/releases/tag/7.2.0

### 包矩阵

| 包 | 来源 | 版本 | 说明 |
| --- | --- | --- | --- |
| PyTorch | [`torch-2.12.0-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torch-2.12.0-cp312-cp312-linux_aarch64.whl) | 2.12.0 | Python 3.12 / aarch64 wheel。 |
| TorchVision | [`torchvision-0.27.0+78839c2-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torchvision-0.27.0%2B78839c2-cp312-cp312-linux_aarch64.whl) | 0.27.0 | 与上方 PyTorch wheel 配套。 |
| ONNX Runtime GPU | [`onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl) | 1.28.0 | 保持 `numpy<2` 约束。 |
| TensorRT | 系统 Python 包 | 10.16.2.10 | 通过 `--system-site-packages` 复用。 |
| OpenCV | 系统 Python 包 | 5.0.0 | 通过 `--system-site-packages` 复用。 |

### 创建环境

JetPack 7 通过 `--system-site-packages` 复用系统 TensorRT 和 OpenCV 包。

```bash
uv venv .venv --python 3.12 --system-site-packages
source .venv/bin/activate
```

### 安装 Wheels

安装 JP7 wheels：

```bash
uv pip install \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torch-2.12.0-cp312-cp312-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/torchvision-0.27.0%2B78839c2-cp312-cp312-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/7.2.0/onnxruntime_gpu-1.28.0-cp312-cp312-linux_aarch64.whl" \
  "numpy<2"
```

### 验证

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

这些 wheels 已在 JetPack 6.2.1 rc1 上验证，但不保证跨 JetPack 6.x 小版本完全兼容。

### 包矩阵

| 包 | 来源 | 版本 | 说明 |
| --- | --- | --- | --- |
| PyTorch | [`torch-2.3.0a0+git97ff6cf-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torch-2.3.0a0%2Bgit97ff6cf-cp310-cp310-linux_aarch64.whl) | 2.3.0a0 | Python 3.10 / aarch64 wheel。 |
| TorchVision | [`torchvision-0.18.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchvision-0.18.0-cp310-cp310-linux_aarch64.whl) | 0.18.0 | 与上方 PyTorch wheel 配套。 |
| Torchaudio | [`torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl) | 0.18.0 | Jetson 精简构建。 |
| ONNX Runtime GPU | [`onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl`](https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl) | 1.24.0 | CUDA / TensorRT GPU 构建。 |
| TensorRT | 系统 Python 包 | 10.3.0 | 通过 `--system-site-packages` 复用。 |
| OpenCV | 系统 Python 包 | 4.11.0 | 通过 `--system-site-packages` 复用。 |

### 创建环境

JetPack 6 优先推荐通过 `--system-site-packages` 复用系统 TensorRT 和 OpenCV 包。如果你更希望使用完全 wheel 化的环境，也可以手动安装 release 页面中的 TensorRT 和 OpenCV wheels。

```bash
uv venv .venv --python 3.10 --system-site-packages
source .venv/bin/activate
```

### 安装 Wheels

安装 JP6 wheels：

```bash
uv pip install \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torch-2.3.0a0%2Bgit97ff6cf-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchvision-0.18.0-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/torchaudio-0.18.0-cp310-cp310-linux_aarch64.whl" \
  "https://github.com/Shattered217/Jetson-Orin-Wheels/releases/download/6.2.1rc1/onnxruntime_gpu-1.24.0-cp310-cp310-linux_aarch64.whl" \
  "numpy<2"
```

### 验证

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

## YOLO 简单检查

安装 PyTorch 和 OpenCV 后，可以用 Ultralytics YOLO 做一次环境检查：

```bash
uv pip install ultralytics
yolo check
```

输出中应能看到 Jetson GPU、CUDA 可用状态、PyTorch、TorchVision、NumPy、OpenCV 等版本信息。

## 常见问题

- **Python ABI 不匹配**：`cp310` wheels 只能用于 Python 3.10；`cp312` wheels 只能用于 Python 3.12。
- **JetPack 分支不匹配**：请从与当前 JetPack 对应的 release tag 安装 wheels。
- **NumPy 兼容性**：使用 ONNX Runtime GPU wheels 时，请保持 `numpy<2` 约束。
- **TensorRT / OpenCV 导入失败**：使用 `--system-site-packages` 重新创建环境。
- **存在多个 Python 环境**：安装前先运行 `which python`、`python --version`、`python -m pip --version` 确认当前解释器。

## 参考

- [Jetson Orin Wheels releases](https://github.com/Shattered217/Jetson-Orin-Wheels/releases)
- [Jetson Python 环境优雅链接系统包：uv `--system-site-packages`](https://nvcc-v.com/2026/06/09/jetson-python-uv-system-site-packages/)
- [PyTorch for Jetson](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048)
- [TensorRT Python package source](https://github.com/NVIDIA/TensorRT/tree/release/10.3/python)
