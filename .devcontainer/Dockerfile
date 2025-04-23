FROM mcr.microsoft.com/devcontainers/base:debian

# Add CRAN repo for R 4.4+ and install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        dirmngr \
        gnupg \
        ca-certificates \
        curl \
        software-properties-common \
        apt-transport-https && \
    curl -fsSL https://cloud.r-project.org/bin/linux/debian/bookworm-cran40/cran.gpg | gpg --dearmor -o /usr/share/keyrings/cran.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/cran.gpg] https://cloud.r-project.org/bin/linux/debian bookworm-cran40/" > /etc/apt/sources.list.d/cran.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends r-base

# Download the latest installer
ADD https://astral.sh/uv/install.sh /uv-installer.sh

# Run the installer then remove it
RUN sh /uv-installer.sh && rm /uv-installer.sh

# Install uv and uvx to /usr/local/bin
RUN install -m 755 ~/.local/bin/uv /usr/local/bin/uv \
&& install -m 755 ~/.local/bin/uvx /usr/local/bin/uvx

# Install Quarto
RUN curl -LO https://quarto.org/download/latest/quarto-linux-amd64.deb && \
    dpkg -i quarto-linux-amd64.deb && \
    rm quarto-linux-amd64.deb
