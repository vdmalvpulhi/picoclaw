# picoclaw

A fork of [sipeed/picoclaw](https://github.com/sipeed/picoclaw) — a lightweight claw machine controller service written in Go.

## Overview

Picoclaw provides a backend service for controlling claw machine hardware, managing game sessions, handling coin/token input, and streaming live video to players.

## Features

- Hardware control via serial/GPIO interface
- WebSocket-based real-time game session management
- Live video streaming support
- Coin/token validation and session tracking
- Configurable game parameters (claw strength, time limits, etc.)
- REST API for admin management

## Requirements

- Go 1.21+
- Docker & Docker Compose (for containerized deployment)
- Compatible claw machine hardware (or simulator mode)

## Getting Started

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/your-org/picoclaw.git
   cd picoclaw
   ```

2. Copy the example environment file and configure it:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. Install dependencies:
   ```bash
   go mod download
   ```

4. Run the service:
   ```bash
   go run ./cmd/picoclaw
   ```

### Docker

```bash
docker compose up --build
```

## Configuration

All configuration is done via environment variables. See [`.env.example`](.env.example) for available options.

| Variable | Description | Default |
|---|---|---|
| `SERVER_PORT` | HTTP server listen port | `8080` |
| `LOG_LEVEL` | Log verbosity (`debug`, `info`, `warn`, `error`) | `info` |
| `HARDWARE_PORT` | Serial port for hardware communication | `/dev/ttyUSB0` |
| `SIMULATOR_MODE` | Run without physical hardware | `false` |
| `SESSION_TIMEOUT` | Game session timeout in seconds | `120` |

## API

### REST Endpoints

| Method | Path | Description |
|---|---|---|
| `GET` | `/health` | Health check |
| `GET` | `/api/v1/status` | Machine status |
| `POST` | `/api/v1/session/start` | Start a new game session |
| `POST` | `/api/v1/session/end` | End current session |
| `GET` | `/api/v1/admin/config` | Get machine configuration |
| `PUT` | `/api/v1/admin/config` | Update machine configuration |

### WebSocket

- `ws://<host>/ws/game` — Real-time game control and state updates
- `ws://<host>/ws/stream` — Live video stream

## Contributing

Please read our [pull request template](.github/pull_request_template.md) before submitting changes. Bug reports and feature requests should use the appropriate issue templates.

## License

MIT License — see [LICENSE](LICENSE) for details.
