# Install PyTorch 2.6 with CUDA 12.4
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# Install Ubuntu packages
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y rsync git git-lfs curl ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Install uv
COPY --from=ghcr.io/astral-sh/uv:0.6 /uv /uvx /usr/bin/
# Prevent uv to create .venv. This will install packages in the system Python environment
# https://docs.astral.sh/uv/concepts/projects/config/#project-environment-path
# python -c "import sysconfig; print(sysconfig.get_config_var('prefix'))"  # /opt/conda
ENV UV_SYSTEM_PYTHON=1 \
    UV_NO_CACHE=1 \
    UV_PROJECT_ENVIRONMENT=/opt/conda \
    UV_LINK_MODE=copy
RUN echo 'eval "$(uv generate-shell-completion bash)"' >> /root/.bashrc
RUN echo 'eval "$(uvx --generate-shell-completion bash)"' >> /root/.bashrc

# Install Python packages
# There are three options to install Python packages

# (1) uv pip install with requirements.txt
# COPY requirements.txt requirements.txt
# RUN uv pip install --system --no-cache -r requirements.txt

# (2) uv sync with uv.lock
# COPY . .
# RUN uv lock  # run this first to generate uv.lock, then comment it out
# RUN uv sync --frozen  # if uv.lock has been generated, uncomment this line

# (3) uv sync with pyproject.toml without uv.lock
COPY . .
RUN uv sync --python 3.11
