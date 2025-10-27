Blue/Green Deployment with Nginx Auto-Failover
Overview
This project implements a Blue/Green deployment strategy with automatic failover using Nginx as a reverse proxy. The setup ensures zero-downtime deployments and automatic traffic switching when failures occur.

Quick Start
Clone and setup

git clone https://github.com/BAGHIRA-0F-RELIGIONS/hng13-stage2-devops
cd hng13-stage2-devops/
Configure environment Edit .env with your image references and release IDs.

Deploy

sudo docker-compose up -d --build
Verify deployment
curl http://localhost:8080/version
Testing Failover
Initial state (Blue active)
curl http://localhost:8080/version
# Response: X-App-Pool: blue
Verify automatic failover
curl http://localhost:8080/version
# Response: X-App-Pool: green (automatic switch)
Stop chaos
curl -X POST http://localhost:8081/chaos/stop
Architecture
Nginx: Reverse proxy with upstream failover configuration
Blue Service: Primary application instance (port 8081)
Green Service: Backup application instance (port 8082)
Health Checks: Automatic failure detection
Retry Logic: Seamless failover within same client request
Key Features
Automatic health-based failover
Zero failed client requests during failover
Header preservation (X-App-Pool, X-Release-Id)
Configurable timeouts and retry policies
Docker Compose orchestration