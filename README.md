# Cloud-1: Automated WordPress Deployment

## Project Overview
Cloud-1 is an automated deployment system for WordPress, inspired by the 42 school "Inception" project. This project deploys a complete WordPress environment (including WordPress, MySQL, and PHPMyAdmin) using Docker containers with an automated setup process.

## Architecture Diagram
<img src="./images/Architecture Diagram.png"/>

## Deployment Roadmap
<img src="./images/Deployment Roadmap.png"/>

## Key Features
- **Fully Automated Deployment**: One-command setup using Ansible
- **Containerized Architecture**: Each process runs in its own Docker container
- **Persistent Data**: All website data persists through server reboots
- **Secure Configuration**: Restricted access to critical services
- **TLS Support**: HTTPS connections for secure browsing
- **Scalable**: Can be deployed across multiple servers simultaneously

## Technologies Used
- **Docker & Docker Compose**: Container management
- **Ansible**: Automation tool for deployment
- **WordPress**: Content management system
- **MySQL**: Database backend
- **PHPMyAdmin**: Database management interface
- **Nginx**: Web server and reverse proxy

## Prerequisites
- Ubuntu 20.04 LTS (server)
- SSH access to the server
- Python installed on the server
- Ansible installed on your local machine

## Project Structure
```
cloud-1/
├── ansible/
│   ├── inventory.ini       # Server inventory for Ansible
│   └── main.yml            # Main Ansible playbook
├── tasks/
│   ├── create_app_directory.yml
│   ├── copy_files_to_compose.yml
│   ├── install_docker.yml
│   ├── install_docker_dependencies.yml
│   ├── add_docker_key.yml
│   ├── add_docker_repository.yml
│   ├── install_docker_compose.yml
│   ├── start_docker_service.yml
│   ├── add_user_to_docker_group.yml
│   ├── create_startup_script.yml
│   ├── add_startup_script_to_crontab.yml
│   ├── run_phpmyadmin_from_docker.yml
│   ├── run_compose_app.yml
│   └── remove_docker_and_related_packages.yml
├── app/
│   ├── docker-compose.yml  # Docker Compose configuration
│   ├── wordpress.conf      # WordPress Nginx configuration
│   └── .env                # Environment variables for Docker Compose
├── diagrams/
│   ├── architecture.png    # Architecture diagram
│   └── roadmap.png         # Deployment roadmap diagram
└── README.md              # Project documentation
```

## Deployment Steps
1. Clone this repository
2. Update the inventory file with your server IP
3. Configure the environment variables in `.env`
4. Run the Ansible playbook:
   ```
   ansible-playbook -i ansible/inventory.ini ansible/main.yml
   ```

## Docker Compose Configuration
The project deploys the following containers:
- **WordPress**: PHP and WordPress application
- **MySQL**: Database server
- **PHPMyAdmin**: Web interface for MySQL management
- **Nginx**: Reverse proxy with TLS support

## Environmental Variables
All sensitive information is stored in the `.env` file:
- `MYSQL_ROOT_PASSWORD`: Root password for MySQL
- `MYSQL_DATABASE`: WordPress database name
- `MYSQL_USER`: WordPress database user
- `MYSQL_PASSWORD`: WordPress database password
- `WORDPRESS_DB_HOST`: Database hostname
- `WORDPRESS_DB_NAME`: WordPress database name
- `WORDPRESS_DB_USER`: WordPress database user
- `WORDPRESS_DB_PASSWORD`: WordPress database password

## Networking
- Web traffic is served on ports 80 (HTTP) and 443 (HTTPS)
- PHPMyAdmin is accessible through the web interface
- MySQL is not directly accessible from outside the Docker network

## Data Persistence
All data is stored in Docker volumes:
- WordPress files: `/var/www/html`
- MySQL database: `/var/lib/mysql`

## Restart Policy
All containers are configured to restart automatically if the server reboots, ensuring continuous service availability.

## Security Features
- MySQL is only accessible from within the Docker network
- TLS certificates for secure HTTPS connections
- Restricted access to sensitive services

## Troubleshooting
- Check container status: `docker ps`
- View container logs: `docker logs <container_name>`
- Restart a specific container: `docker restart <container_name>`
- Restart all containers: `docker-compose -f /app/docker-compose.yml restart`

## Acknowledgements
- Based on the 42 school "Inception" project
- Leverages Ansible for automation
- Uses Docker and Docker Compose for containerization