# Docker Observability Lab

Observability Lab include:
* **Prometheus** for time-series metric collection
* **Grafana** for visualizing those metrics
* **Node Exporter** instances to simulate multiple hosts
* **Alertmanager** for triggering alerts based on thresholds

## Pre-requisite
* Docker & Docker Compose installed
* A basic understanding of container networking
* Some curiosity and \~5 minutes of your time

## Folder Structure
```bash
observability-lab/
├── docker-compose.yml
└── conf/
    ├── grafana/
    │   ├── datasources/
    │   │   └── datasources.yaml 
    │   └── dashboards/
    │       ├── dashboards.yaml
    │       └── node_exporter_dashboard.json
    └── prometheus/
        ├── prometheus.yml
        ├── alerts.rules.yml
        └── alertmanager.yml
```

## Running the Lab

Clone Repository
```bash
git clone https://github.com/Kartikdudeja/observability-lab.git
```

From the root of your project:

```bash
docker-compose up -d
```

Check the status:

```bash
docker-compose ps
```

You should see five running containers. Now visit:

* **Prometheus** → [http://localhost:9090](http://localhost:9090)
* **Grafana** → [http://localhost:3000](http://localhost:3000)
* **Alertmanager** → [http://localhost:9093](http://localhost:9093)

Default Grafana login:

* **User**: `admin`
* **Password**: `admin`

## Triggering Alerts

Try stopping one of the Node Exporter containers:

```bash
docker-compose stop node-exporter-1
```

Within 30 seconds, Prometheus will trigger an alert that flows to Alertmanager.

## Tearing It Down

Once done, you can remove the environment with:

```bash
docker-compose down -v
```

This will also delete volumes. Skip the `-v` flag if you want to preserve your data.
