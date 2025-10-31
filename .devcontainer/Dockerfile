FROM mcr.microsoft.com/devcontainers/universal:3

# Instalar herramientas adicionales
RUN apt-get update && apt-get install -y \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Variables
ENV NODE_ENV=development
