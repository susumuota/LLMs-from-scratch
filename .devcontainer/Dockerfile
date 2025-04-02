# Install PyTorch 2.6 with CUDA 12.4
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# Install Ubuntu packages
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y rsync git curl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Install uv
COPY --from=ghcr.io/astral-sh/uv:0.6 /uv /uvx /usr/bin/
ENV UV_SYSTEM_PYTHON=1 \
    UV_PROJECT_ENVIRONMENT=/opt/conda \
    UV_LINK_MODE=copy
RUN echo 'eval "$(uv generate-shell-completion bash)"' >> /root/.bashrc
RUN echo 'eval "$(uvx --generate-shell-completion bash)"' >> /root/.bashrc

# Install Python packages
# COPY requirements.txt requirements.txt
# RUN uv pip install --system --no-cache -r requirements.txt
COPY . .
# RUN uv lock
# RUN uv sync --frozen
RUN uv sync --dev --python 3.11
