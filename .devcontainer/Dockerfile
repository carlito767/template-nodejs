FROM node:18.17.1-buster

# Args
ARG PNPM_VERSION=8.6.12

# Envs
ENV PNPM_VERSION=${PNPM_VERSION}

# Set working directory
WORKDIR /workspace

# Update npm and install pnpm
RUN npm i -g npm@latest && \
  npm install -g pnpm@$PNPM_VERSION && \
  pnpm config set store-dir .pnpm-store

# Fetch packages from lockfile into virtual store, package manifest is ignored
COPY .npmrc pnpm-lock*.yaml ./
RUN pnpm fetch

# Copy project files and install dependencies from virtual store
COPY . ./
RUN pnpm install -r --offline
