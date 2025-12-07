# ===== 1. Base image with Python =====
FROM python:3.10-slim

# ===== 2. Install system packages =====
RUN apt-get update && apt-get install -y \
    git \
    ffmpeg \
    wget \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# ===== 3. Create Colab-like /content directory =====
WORKDIR /content

# ===== 4. Install Python dependencies =====
COPY requirements.txt /content/requirements.txt
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# ===== 5. Enable ipywidgets in Jupyter Lab (JupyterLab 4+ usually ok) =====
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix || true

# ===== 6. Expose Jupyter port =====
EXPOSE 8888

# ===== 7. Start Jupyter Lab when container runs =====
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=", "--NotebookApp.password="]
