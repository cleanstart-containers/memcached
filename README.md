# CleanStart Container for Memcached

Enterprise-grade Memcached distributed memory caching system container optimized for high-performance caching scenarios. This container includes the latest stable Memcached server with security hardening and enterprise features. Memcached is an in-memory key-value store for small chunks of arbitrary data from results of database calls, API calls, or page rendering. The container is configured for optimal performance in distributed systems with support for multiple protocols and authentication mechanisms.

**📌 CleanStart Foundation:** Security-hardened, minimal base OS designed for enterprise containerized environments.

---

## Key Features

- High-performance distributed memory caching
- Multi-threaded architecture for concurrent connections
- Support for multiple protocols (ASCII and binary)
- Enterprise-grade security features and access controls
- Security-hardened base image
- Optimized for distributed systems

---

## Common Use Cases

Typical scenarios where this container excels:

- Database query result caching
- Session storage for web applications
- API response caching
- Distributed caching layer in microservices architecture
- High-performance data caching
- Scalable caching solutions

---

## Quick Start

### Pull Latest Image

Download the container image from the registry:
```bash
docker pull ghcr.io/cleanstart-containers/memcached:latest
docker pull ghcr.io/cleanstart-containers/memcached:latest-dev
```

### Basic Run

Run the container with basic configuration:
```bash
docker run -d --name memcached-instance -p 11211:11211 ghcr.io/cleanstart-containers/memcached:latest
```

### Production Deployment

Deploy with production security settings:
```bash
docker run -d --name memcached-prod \
  --read-only \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  -p 11211:11211 \
  -m 1024m \
  ghcr.io/cleanstart-containers/memcached:latest
```

### Volume Mount

Mount local directory for persistent data:
```bash
docker run -d -v $(pwd)/memcached-data:/data ghcr.io/cleanstart-containers/memcached:latest
```

### Port Forwarding

Run with custom port mappings:
```bash
docker run -d -p 11222:11211 ghcr.io/cleanstart-containers/memcached:latest
```

---

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PATH` | `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` | System PATH configuration |
| `MEMCACHED_MEMORY_LIMIT` | `64` | Maximum memory to use for storage in megabytes |
| `MEMCACHED_CONNECTIONS` | `1024` | Maximum simultaneous connections |

---

## Security & Best Practices

### Recommended Security Context
```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  runAsGroup: 1000
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop: ['ALL']
```

### Best Practices

- Use specific image tags for production (avoid latest)
- Configure resource limits: memory and CPU constraints
- Enable read-only root filesystem when possible
- Run containers with non-root user (--user 1000:1000)
- Use --security-opt=no-new-privileges flag
- Regularly update container images for security patches
- Implement proper network segmentation
- Monitor container metrics for anomalies

---

## Architecture Support

### Multi-Platform Images
```bash
docker pull --platform linux/amd64 ghcr.io/cleanstart-containers/memcached:latest
docker pull --platform linux/arm64 ghcr.io/cleanstart-containers/memcached:latest
```

---

## Resources

- **Official Documentation:** https://memcached.org/
- **Provenance / SBOM / Signature:** https://images.cleanstart.com/images/memcached
- **Docker Hub:** https://hub.docker.com/r/cleanstart/memcached
- **CleanStart All Images:** https://images.cleanstart.com/images/memcached/details
- **CleanStart Community Images:** https://hub.docker.com/u/cleanstart

---

## Vulnerability Disclaimer

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

**Security remains a shared responsibility:** CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
