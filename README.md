# hello-spin-redis

A simple Redis message handler using TinyGo and Fermyon Spin to demonstrate event-driven WebAssembly applications.

## What it does

This application listens for messages published to a Redis channel and processes them using a WebAssembly component compiled with TinyGo.

## Prerequisites

- [Spin CLI](https://developer.fermyon.com/spin/v3/install)
- Go 1.20.5+
- TinyGo 0.33.0+
- Docker (for running Redis)

## Quick Start

### 1. Install dependencies

```bash
# Install Spin
curl -fsSL https://developer.fermyon.com/downloads/install.sh | bash
sudo mv ./spin /usr/local/bin/

# Install/upgrade Go
brew update && brew upgrade go

# Install TinyGo
brew tap tinygo-org/tools
brew install tinygo
```

### 2. Start Redis

```bash
docker run --name redis-server -d -p 6379:6379 redis
```

### 3. Build and run

```bash
spin build --up
```

You should see:
```
Active Channels on redis://127.0.0.1:6379:
redis://127.0.0.1:6379:hello-messages: [hello-message-handler]
```

### 4. Test it

In another terminal, publish a message:

```bash
docker exec -it redis-server redis-cli
127.0.0.1:6379> PUBLISH hello-messages "Hello from Redis!"
```

The message will appear in your Spin application logs.

## Project Structure

- `main.go` - Message handler implementation
- `spin.toml` - Spin application configuration
- `main.wasm` - Compiled WebAssembly binary (generated)

## Configuration

The app listens to Redis at `127.0.0.1:6379` on the `hello-messages` channel. You can modify these settings in `spin.toml`.

## Learn More

Read the full writeup: [Taking TinyGo for a Spin](https://medium.com/@anita.bendelja/taking-tinygo-for-a-spin-9612b67fb6a6)

## Author

Anita Bendelja ([@anitabee](https://github.com/anitabee))
