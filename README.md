# Simple monitoring

This repository runs the Python and Spring REST services alongside Prometheus and Grafana. The application sources remain in their Git submodules; the Dockerfiles and monitoring configuration are managed here.

## Start

From the repository root, build and start the stack:

```sh
docker compose up --build
```

Open Grafana at <http://localhost:3000> (default login: `admin` / `admin`). The provisioned **Services / Service overview** dashboard shows scrape health, request rates, and server error rates for both services. Prometheus is available at <http://localhost:9090>.

The services are available at <http://localhost:8000> (Python) and <http://localhost:8080> (Spring). Generate requests to populate the charts, for example:

```sh
curl http://localhost:8000/
curl http://localhost:8080/
```

Metrics are exposed at <http://localhost:8000/metrics> and <http://localhost:8080/actuator/prometheus>. Grafana and Prometheus data are kept in named Docker volumes.

Stop the stack with `docker compose down`; add `-v` to also remove stored metrics and dashboards.