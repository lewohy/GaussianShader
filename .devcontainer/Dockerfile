FROM nvidia/cuda:12.8.1-cudnn-devel-ubuntu22.04

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

ARG USERNAME=gsshader
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# tzdata interactive 설정 방지
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
# RTX 40xx 타겟
ENV TORCH_CUDA_ARCH_LIST "8.6"

RUN apt-get update && apt-get install -y \
    && apt-get install -y tzdata sudo curl git unzip wget lsb-release software-properties-common gnupg gdb libgl1 \
    && rm -rf /var/lib/apt/lists/*

# create user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL >/etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && chsh -s $(which bash) $USERNAME

USER $USERNAME

