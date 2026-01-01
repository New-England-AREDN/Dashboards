# Dashboards
This repository contains Grafana and other source files for New England AREDN Grafana Dashboards. It can be used for New England AREDN RF dashboard development. New England AREDN dashboards are hosted in production at AB1OC. Prometheus currently provides backend Time Series Database (TSDB) support for the New England AREDN network. Please get in touch with AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you'd like to have your AREDN RF Links, Routers, or Services added to the dashboards.

You can view the Version 1 production RF Link Dashboard at [https://mvara-dash.n1mva.org](https://mvara-dash.n1mva.org).

## Problems and Enhancements

Please submit Issues and suggest feature enhancements via the standard GitHub Problem Report (PR) mechanism. A Template is provided. Please limit the *Issues* you post to topics directly related to the Dashboards in this repo.

## Setting Up a Dashboard Development Environment

### Prerequisites

Our dashboard development environment is based on [Docker Desktop](https://docs.docker.com/desktop/) and [Portainer](https://github.com/portainer/portainer). You should also set up [Watchtower](https://github.com/nicholas-fedor/watchtower)to check for and flag updates to the container images in your development environment. This will ensure that you are using the latest images during development and testing.

You will also need access to the New England production Prometheus Time Series Database (TSDB). Please get in touch with AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) for access.

You can follow these steps to set up the Grafana dashboard development environment:

1. [Install Docker Desktop](https://docs.docker.com/desktop/) on you development machine. If you are doing development on a Windows machine, you will also need to install Windows Subsystem for Linus (WSL). Run Docker Desktop when the installation is complete.
2. Clone this repo using your terminal to create a local ***Dashboards*** development file structure.
   - ```
     git clone https://github.com/New-England-AREDN/Dashboards
     ```
3. Create and edit an environment file for your installation:
   - ```
     cd Dashboards/dev
     cp env.example .env
     <edit> .env  # Set the variables for you development environment
     ```
4. Install Portainer CE using the following commands:
  - ```
    cd ../Tools
    docker compose -f portainer-compose.yml -p portainer-ce up -d
    ```
5. Start Portainer via [https://localhost:9443](https://localhost:9443). Set you password and login to to Portainer.
6. Create a ***Stack*** in Portainer for your Grafana development environment by uploading the provided ***Dashboards/dev/docker-compose.yml*** file and load your ***Dashboard/dev/.env** file to create the environment variables for your stack.
7. Run your Stack to start Grafana. You will be running the Version 1 RF-Dashboard using data from the New England production Prometheus TSDB. You can access Grafana and the current dashboard(s) via [http://localhost:3000](http://localhost:3000).
8. Create and edit an email notification setup for Watchtower:
  - ```
    cd Dashboards/Tools
    cp env.example .env
    <edit> .env  # Set the variable to configure email notifications
    ```
9. Create a ***Stack*** in Portainer for Watchtower named ***watchtower*** by uploading ***Dashboards/Tools/watchtower-compose.yml*** file and load your ***Dashboards/Tools/.env** file to create the environment variables for your stack.
10. You can create or modify your dashboards as .json files in ***Dashboards/dev/provisioning/dashboards***.

## Submitting Changes

You can contribute fixes and changes to the files in this repo via GitHub Pull Requests (PRs). Please document the nature and scope of your proposed changes. _It is best to submit individual changes rather than bundles, as this makes it more likely that we can accept a subset of your changes without requiring resubmission of the entire bundle._
