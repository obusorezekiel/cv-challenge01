# Use a specific Python version
FROM python:3.10-slim

# Install system dependencies and Rust toolchain
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libssl-dev \
    curl \
    && curl https://sh.rustup.rs -sSf | sh -s -- -y \
    && export PATH="/root/.cargo/bin:$PATH" \
    && rustup default stable \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 - \
    && export PATH="/root/.local/bin:$PATH" \
    && poetry --version

# Set the working directory
WORKDIR /app

# Copy application files
COPY . /app

# Install dependencies
RUN poetry config virtualenvs.create false \
    && poetry install

# Expose the application port
EXPOSE 8000

# Start the application
CMD ["bash", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --reload --host 0.0.0.0"]
