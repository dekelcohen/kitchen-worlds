FROM nvidia/cuda:12.2.2-base-ubuntu22.04 

ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /workspace

# ------------------------------------------------------------
# 1. System deps (first apt-get block)
# ------------------------------------------------------------
RUN apt-get update && apt-get install -y \
    libegl1-mesa-dev \
    libgles2-mesa-dev \
    xvfb \
    wget \
    curl \
    git && \
    rm -rf /var/lib/apt/lists/*

# ------------------------------------------------------------
# 2. Install NVM + NodeJS 22 + gemini-cli
# ------------------------------------------------------------
RUN bash -c " \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash && \
    export NVM_DIR=\"$HOME/.nvm\" && \
    . \"$HOME/.nvm/nvm.sh\" && \
    nvm install 22 && \
    npm install -g @google/gemini-cli \
"

# ------------------------------------------------------------
# 3. Install Miniconda (Python 3.10 base env)
# ------------------------------------------------------------
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py310_25.1.1-2-Linux-x86_64.sh && \
    chmod +x Miniconda3-py310_25.1.1-2-Linux-x86_64.sh && \
    ./Miniconda3-py310_25.1.1-2-Linux-x86_64.sh -b -p /opt/conda && \
    rm Miniconda3-py310_25.1.1-2-Linux-x86_64.sh

ENV PATH="/opt/conda/bin:${PATH}"

# Initialize conda (so future shells load it)
RUN conda init bash

# ------------------------------------------------------------
# 4. Install second apt-get block
# ------------------------------------------------------------
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    libeigen3-dev \
    liborocos-kdl-dev \
    libkdl-parser-dev \
    liburdfdom-dev \
    libnlopt-dev \
    libnlopt-cxx-dev \
    swig && \
    rm -rf /var/lib/apt/lists/*

# ------------------------------------------------------------
# 5. Default shell
# ------------------------------------------------------------
CMD ["/bin/bash"]

