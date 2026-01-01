# Dashboards
This repository contains Grafana and other source files for New England AREDN Grafana Dashboards. It can be used for New England AREDN RF dashboard development. New England AREDN dashboards are hosted in production at AB1OC. Prometheus currently provides backend Time Series Database (TSDB) support for the New England AREDN network. Please get in touch with AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) if you'd like to have your AREDN RF Links, Routers, or Services added to the dashboards.

You can view the Version 1 production RF Link Dashboard at [https://mvara-dash.n1mva.org](https://mvara-dash.n1mva.org).

## Problems and Enhancements

Please submit Issues and suggest feature enhancements via the standard GitHub Problem Report (PR) mechanism. A Template is provided. Please limit the *Issues* you post to topics directly related to the Dashboards in this repo.

## Setting Up a Dashboard Development Environment

### Prerequisites

Our dashboard development environment is based on [Docker Desktop](https://docs.docker.com/desktop/) and [Portainer](https://github.com/portainer/portainer). You should install these tools before setting up your development environment. You can also set up a [Watchtower](https://github.com/nicholas-fedor/watchtower) stack to check for and flag updates to the Docker images in your development environment.

You will also need access to the New England production Prometheus Time Series Database (TSDB). Please get in touch with AB1OC at [ab1oc@arrl.org](mailto:ab1oc@arrl.org) for access.

Once you have Docker Desktop and Portainer running and you have access to the Prometheus TSDB, you can follow these steps to set up the Grafana dashboard development environment:

1. Clone this repo to create a local ***Dashboards*** development file structure.
   - ```
     git clone https://github.com/New-England-AREDN/Dashboards
     ```
2. Create and edit an environment file for your installation
   - ```
     cd Dashboards/dev
     cp env.example .env
     <edit> .env  # Set the variables for you dev environment
     ```
3. Create a ***Stack*** in Portainer by uploading the provided ***Dashboards/dev/docker-compose.yml*** file and load your ***.env** file to create the environment variables for your stack.
4. Run your Stack to start Grafana. You will be running the Version 1 RF-Dashboard using data from the New England production Prometheus TSDB. You can access Grafana and the current dashboard(s) via [http://localhost:3000](http://localhost:3000).
5. You can create or modify your dashboards as .json files in ***Dashboards/dev/provisioning/dashboards***.

## Submitting Changes

You can contribute fixes and changes to the files in this repo via GitHub Pull Requests (PRs). Please document the nature and scope of your proposed changes. _It is best to submit individual changes rather than bundles, as this makes it more likely that we can accept a subset of your changes without requiring resubmission of the entire bundle._
