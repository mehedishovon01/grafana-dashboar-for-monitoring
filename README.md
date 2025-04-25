# Monitoring Stack

This repository contains a monitoring stack using Prometheus, Grafana, Node Exporter, and Blackbox Exporter to monitor various services and system metrics.

## Components

1. **Prometheus** - Time series database and monitoring system
   - Port: 9090
   - Configuration: `prometheus/prometheus.yml`

2. **Grafana** - Visualization and dashboard platform
   - Port: 3010
   - Default credentials:
     - Username: admin
     - Password: secret

3. **Node Exporter** - System metrics exporter
   - Port: 9100
   - Collects CPU, memory, disk, and network metrics

4. **Blackbox Exporter** - HTTP/HTTPS monitoring
   - Port: 9115
   - Configuration: `blackbox/config.yml`

## Monitored Services
- Github Site (https://github.com)
- Linkedin (https://linkedin.com)
- Facebook (https://facebook.com)

## Setup Instructions

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd Monitoring
   ```

2. Start the monitoring stack:
   ```bash
   docker-compose up -d
   ```

3. Access the services:
   - Prometheus: http://localhost:9090
   - Grafana: http://localhost:3010
   - Node Exporter metrics: http://localhost:9100/metrics
   - Blackbox Exporter: http://localhost:9115

## Configuration

### Prometheus Configuration
- Located in `prometheus/prometheus.yml`
- Scrapes metrics from Node Exporter and Blackbox Exporter
- Monitors HTTP endpoints for availability

### Blackbox Configuration
- Located in `blackbox/config.yml`
- Configures HTTP/HTTPS probe settings
- Uses http_2xx module for endpoint monitoring

### Node Exporter Configuration
- Collects system metrics from the host
- Mounts necessary system directories
- Excludes certain mount points from filesystem metrics

## Monitoring Features

1. **System Metrics**
   - CPU usage
   - Memory utilization
   - Disk I/O
   - Network traffic
   - System load

2. **Service Monitoring**
   - HTTP/HTTPS endpoint availability
   - Response time
   - Status codes
   - SSL certificate validity

## Maintenance

### Updating Configuration
1. Modify the respective configuration files
2. Reload Prometheus configuration:
   ```bash
   curl -X POST http://localhost:9090/-/reload
   ```

### Adding New Services
1. Add new targets to `prometheus/prometheus.yml`
2. Reload Prometheus configuration

### Backup
- Grafana data is persisted in a Docker volume
- Configuration files are version controlled

## Troubleshooting

1. **No Data in Grafana**
   - Check if Prometheus targets are up
   - Verify network connectivity between services
   - Check service logs: `docker-compose logs <service-name>`

2. **Service Not Responding**
   - Check if the service is running: `docker-compose ps`
   - View service logs: `docker-compose logs <service-name>`
   - Verify port mappings and network configuration

## Security Notes

- Grafana password is set to 'secret' by default - change in production
- Services are running in a dedicated Docker network
- HTTPS endpoints are monitored for certificate validity
- System metrics are collected with read-only access

## Grafana Dashboard Management

### Importing Dashboards

1. **Access Grafana**
   - Open your web browser and navigate to http://localhost:3010
   - Log in with the default credentials:
     - Username: admin
     - Password: secret

2. **Import Dashboard**
   - Click on the "+" icon in the left sidebar
   - Select "Import" from the dropdown menu
   - In the "Import via grafana.com" field, enter the dashboard ID (e.g., 7587)
   - Click the "Load" button

3. **Configure Data Source**
   - In the import configuration screen:
     - Select your Prometheus data source from the dropdown menu
     - Review and adjust any dashboard variables if needed
   - Click "Import" to add the dashboard to your Grafana instance

4. **Verify Dashboard**
   - The dashboard should now appear in your Grafana instance
   - Check that all panels are displaying data correctly
   - Adjust time range and refresh settings as needed

### Recommended Dashboards

1. **Node Exporter Full** (ID: 1860)
   - Comprehensive system metrics dashboard
   - Includes CPU, memory, disk, and network monitoring
   - Tags: linux, system

2. **Blackbox Exporter** (ID: 7587)
   - HTTP/HTTPS endpoint monitoring
   - Response time and availability metrics
   - Tags: blackbox, prometheus, http/https

3. **Prometheus 2.0 Overview** (ID: 3662)
   - Prometheus server metrics
   - Scrape targets and configuration status
   - Tags: prometheus, monitoring

4. **Blackbox Exporter (HTTP prober)** (ID: 9965)
   - Detailed HTTP/HTTPS monitoring
   - Response time, status codes, and SSL metrics
   - Tags: blackbox, prometheus, web

5. **Website Monitoring** (ID: 13659)
   - Comprehensive website availability monitoring
   - Uptime, response time, and status tracking
   - Tags: blackbox, prometheus, web

6. **Wonderful HTTP Status and Overview** (ID: 13659)
   - Detailed HTTP/HTTPS status monitoring
   - Response time, status codes, and SSL metrics
   - Tags: blackbox, prometheus, web

### Dashboard Customization

1. **Modify Panels**
   - Click on panel title to edit
   - Adjust queries, visualization, and thresholds
   - Save changes to update dashboard

2. **Add New Panels**
   - Click "Add Panel" button
   - Choose visualization type
   - Configure metrics and queries
   - Save to dashboard

3. **Dashboard Settings**
   - Access via dashboard settings icon
   - Modify title, tags, and time settings
   - Configure variables and templating
   - Set refresh intervals

### Troubleshooting Dashboards

1. **No Data Displayed**
   - Verify Prometheus data source is working
   - Check metric names and queries
   - Ensure time range is appropriate
   - Verify scrape targets are up

2. **Panel Errors**
   - Check query syntax
   - Verify metric names exist
   - Ensure proper data source selection
   - Check for rate() function issues

3. **Performance Issues**
   - Reduce query time range
   - Optimize queries
   - Adjust refresh intervals
   - Consider using dashboard caching
