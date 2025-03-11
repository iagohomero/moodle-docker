# Moodle Docker

## Overview
Moodle Docker is a project that simplifies the installation and deployment of Moodle using Docker. With just one command, you can have a fully functional Moodle instance up and running.

## Features
- Easy setup with Docker Compose
- Uses Moodle version **4.5.2 stable**
- Pre-configured environment for quick deployment

## Installation
### Prerequisites
- Docker installed on your system
- Docker Compose installed

### Quick Start
Run the following command in your terminal:
```sh
docker compose up -d --build
```
This will build and start the Moodle instance in detached mode.

## Accessing Moodle
Once the containers are running, you can access Moodle via:
```
http://localhost
```
or, if using a configured domain, replace `localhost` with your domain.

## Stopping the Containers
To stop the running containers, use:
```sh
docker compose down
```

## Contributing
Feel free to contribute to this project by submitting issues or pull requests.

