# Phase 2 - Elasticsearch Installation

## Objective

Deploy Elasticsearch on the Ubuntu Server virtual machine to serve as the central search and analytics engine for the Elastic SIEM.

## Implementation

The installation was performed using Elastic's official documentation, which could be found [here](https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-elasticsearch-with-debian-package).

### Import the Elastic GPG Key

Elastic's public GPG key was imported so Ubuntu could verify the authenticity and integrity of packages downloaded from the official Elastic repository before installation.

### Configure the Elastic APT Repository

The official Elastic APT repository was added so Elasticsearch can be installed and managed through Ubuntu's package manager (apt). This simplifies the installation process and makes it easier to install future updates through Ubuntu's package manager.

### Install Elasticsearch

Elasticsearch was installed using the official Debian package from Elastic's APT repository. During installation, the package created the core components required for the service to operate, including:

- The Elasticsearch application
- A dedicated elasticsearch system user and group
- A `systemd` service for managing Elasticsearch
- Configuration files stored in `/etc/elasticsearch`
- Log files stored in `/var/log/elasticsearch`
- Data storage located in `/var/lib/elasticsearch`
- Default security configuration and TLS certificates

### Enable the Service

The `elasticsearch.service` unit was first enabled to ensure Elasticsearch starts automatically whenever the server boots. The service was then started so Elasticsearch could begin running immediately without requiring a reboot.

## Verification

- Verified GPG key import
```
locate elasticsearch
```
- Verified repository configuration
```
cat /etc/apt/sources.list.d/elastic-9.x.list
OR
apt policy elasticsearch
```
- Verified Elasticsearch service was active
```
sudo systemctl status elasticsearch
```
- Verified Elasticsearch was listening on TCP port 9200
```
sudo ss -tulpn | grep 9200
```
- Verified configuration, log, and data directories existed
```
sudo ls -l /etc/elasticsearch/
sudo ls -l /var/log/elasticsearch/
sudo ls -l /var/lib/elasticsearch/
```

## Key Takeaways

- Elastic packages are signed with a GPG key to ensure package authenticity.
- Installing from the official APT repository simplifies updates and package management.
- Elasticsearch is installed as a systemd service and can be managed using `systemctl`.
- Verifying each installation step before proceeding helps identify issues early and ensures a reliable deployment process.
