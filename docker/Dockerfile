FROM odoo:18.0

# Switch to root to install packages
USER root

# Install pip, venv, and build tools, then install debugpy bypassing Debian restriction
RUN apt-get update && \
    apt-get install -y python3-pip python3-venv build-essential && \
    pip3 install --break-system-packages debugpy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Switch back to odoo user
USER odoo

# Set working directory to mounted Odoo folder
WORKDIR /mnt/odoo