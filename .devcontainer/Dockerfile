# Install PyTorch 2.5 with CUDA 12.4
FROM pytorch/pytorch:2.5.0-cuda12.4-cudnn9-runtime

# Install Ubuntu packages
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y rsync git curl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Install uv
ADD https://astral.sh/uv/install.sh /uv-installer.sh
RUN sh /uv-installer.sh && rm /uv-installer.sh
ENV PATH="/root/.local/bin/:$PATH"
ENV UV_LINK_MODE=copy
RUN echo 'eval "$(uv generate-shell-completion bash)"' >> /root/.bashrc
RUN echo 'eval "$(uvx --generate-shell-completion bash)"' >> /root/.bashrc

# Install Python packages
COPY requirements.txt requirements.txt
RUN uv pip install --system --no-cache -r requirements.txt
