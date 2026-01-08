# Dashboards
This repository contains Grafana and other source files for New England AREDN Grafana Dashboards. It can be used for New England AREDN dashboard development. New England AREDN dashboards are hosted in production at AB1OC. Prometheus currently provides backend Time Series Database (TSDB) support for the New England AREDN network. Please get in touch with AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you'd like to have your AREDN RF Links, Routers, or Services added to the dashboards.

You can view the Version 1 production RF Link Dashboard at [https://rfperf.ne-aredn.net](https://rfperf.ne-aredn.net).

##Network Configuration Data

We also provide JSON configuration data for all of the nodes on the New England AREDN network. This data is accessible via a REST API and is automatically updated when the network configuration changes. The [Configuration and Metrics Data](Configuration-Metrics.md) file in this repository explains the data format and how to access it.

## Accessing the Node Metrics and Configuration Data

The AREDN Node and other metrics, and the Network Configuration JSON data are accessible via the web. Please contact AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you'd like to contribute to the New England AREDN dashboard and monitoring development effort.

## Problems and Enhancements

Please submit Issues and suggest feature enhancements via the standard GitHub Issue Tracker. A Template is provided. Please limit the *Issues* you post to topics directly related to the Dashboards in this repo.

## Setting Up a Dashboard Development Environment

### Prerequisites

Our dashboard development environment is based on [Docker Desktop](https://docs.docker.com/desktop/) and [Portainer](https://github.com/portainer/portainer). You should also set up [Watchtower](https://github.com/nicholas-fedor/watchtower)to check for and flag updates to the container images in your development environment. This will ensure you use the latest images during development and testing.

You will also need access to the New England production Prometheus Time Series Database (TSDB). Please contact AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) for access.

You can follow these steps to set up the Grafana dashboard development environment:

1. [Install Docker Desktop](https://docs.docker.com/desktop/) on you development machine. If you are doing development on a Windows machine, you will also need to install [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/about). Start Docker Desktop when the installation is complete.
2. Clone this repo using your ***shell terminal*** to create a local ***Dashboards*** development file structure.
   - ```
     git clone https://github.com/New-England-AREDN/Dashboards
     ```
3. Create and edit an environment file for your installation:
   - ```
     cd Dashboards/dev
     cp env.example .env
     <edit> .env  # Set the variables for your development environment
     ```
4. Install Portainer CE using the following commands:
   - ```
     cd ../Tools
     docker compose -f portainer-compose.yml -p portainer-ce up -d
     ```
5. Start Portainer via [https://localhost:9443](https://localhost:9443). Next, set your Portainer password and log in to Portainer. Click ***Get Started*** to use Portainer on your machine. Click on ***local*** to access your Docker Desktop environment.
6. Create a ***Stack*** in Portainer for your Grafana development environment by uploading the provided ***Dashboards/dev/docker-compose.yml*** file and loading your ***Dashboard/dev/.env** file to create the environment variables for your stack.
7. Run your Stack to start Grafana. Access Grafana via [http://localhost:3000](http://localhost:3000). Log in as admin/admin and set your Grafana password. Select ***Dashboards *** from the list on the left. Then choose ***Combined Dashboard***.  You will be running the Version 1 RF-Dashboard using data from the New England production Prometheus TSDB.
8. Next, install Watchtower. Begin by creating and editing an email notification setup for Watchtower. Return to your ***Terminal*** and run the following commands:
   - ```
     # Start in Dashboards/Tools
     cp env.example .env
     <edit> .env  # Set the variable to configure email notifications
     ```
9. Create a ***Stack*** in Portainer for Watchtower named ***watchtower*** by uploading ***Dashboards/Tools/watchtower-compose.yml*** file and then loading your ***Dashboards/Tools/.env** file to create the environment variables for your stack.
10. Congratulations! Your development environment is ready to go. You can create or modify your dashboards as .json files in ***Dashboards/dev/provisioning/dashboards***.

## Submitting Changes

You can contribute fixes and changes to the files in this repo via GitHub Pull Requests (PRs). Please document the nature and scope of your proposed changes. _It is best to submit individual changes rather than bundles, as this makes it more likely that we can accept a subset of your changes without requiring resubmission of the entire bundle._
