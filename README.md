# 🚀 Cloud-1: Automated WordPress Deployment

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-%23117AC9.svg?style=for-the-badge&logo=WordPress&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)

## 📋 Project Overview
Cloud-1 is an automated deployment system for WordPress, inspired by the 42 school "Inception" project. This project deploys a complete WordPress environment (including WordPress, MySQL, and PHPMyAdmin) using Docker containers with an automated setup process powered by Ansible.

## 🏗️ Architecture Diagram
<img src="./images/Architecture Diagram.png"/>

## 🛣️ Deployment Roadmap
<img src="./images/Deployment Roadmap.png"/>

## ✨ Key Features
- **🤖 Fully Automated Deployment**: One-command setup using Ansible
- **📦 Containerized Architecture**: Each process runs in its own Docker container
- **💾 Persistent Data**: All website data persists through server reboots
- **🔒 Secure Configuration**: Restricted access to critical services
- **🔐 TLS Support**: HTTPS connections for secure browsing
- **📈 Scalable**: Can be deployed across multiple servers simultaneously

## 🛠️ Technologies Used
- **Docker & Docker Compose**: Container management
- **Ansible**: Automation tool for deployment
- **WordPress**: Content management system
- **MySQL**: Database backend
- **PHPMyAdmin**: Database management interface
- **Nginx**: Web server and reverse proxy

## 🤖 Ansible Automation
Ansible is the cornerstone of this project's automation strategy. Here's how it works:

### Why Ansible?
- **🔌 Agentless Architecture**: No need to install software on target servers
- **🔄 Idempotent Operations**: Can safely run multiple times with same result
- **📝 YAML-based Playbooks**: Easy to read and maintain
- **🌐 Multi-server Support**: Can deploy to multiple targets simultaneously
- **📢 Declarative Syntax**: Define the desired state, not steps

### Ansible Components Used
- **📚 Playbooks**: Series of tasks defining the deployment process
- **📋 Tasks**: Individual operations performed on target servers
- **🔔 Handlers**: Actions triggered by task changes
- **📊 Inventory**: List of managed servers
- **⚙️ Variables**: Configuration values for customization

### Ansible Workflow
1. **🏗️ Infrastructure Setup**: Install Docker and dependencies
2. **📂 File Transfer**: Copy necessary configuration files
3. **⚙️ Service Configuration**: Set up environment variables
4. **🚀 Deployment**: Build and launch Docker containers
5. **✅ Verification**: Ensure services are running properly

### Key Ansible Tasks
- Installing Docker and Docker Compose
- Creating application directories
- Copying configuration files
- Setting up system startup scripts
- Launching containers with Docker Compose
- Configuring automatic service restart

## 📋 Prerequisites
- Ubuntu 20.04 LTS (server)
- SSH access to the server
- Ansible installed on your local machine

## 📁 Project Structure
```
cloud-1/
├── roles/
│   ├── down_app/tasks/
│   │   └── main.yaml
│   ├── install_docker/tasks/
│   │   └── main.yaml
│   ├── nginx/tasks/
│   │   └── main.yaml
│   ├── restart_container/tasks/
│   │   └── main.yaml
│   ├── run_app/
│   │   ├── tasks/
|   |   |   └── main.yaml
│   |   └── files/wordpress_files/
│   │       ├── nginx/conf.d/
│   │       |   └── wordpress.conf
│   |       └── docker-compose.yaml
│   ├── run_database/tasks/
│   │   └── main.yaml
│   ├── run_phpmyadmin/tasks/
│   │   └── main.yaml
│   ├── uninstall_docker/tasks/
│   │   └── main.yaml
│   └── wordpress/tasks/
│       └── main.yaml
├── inventory.ini
├── main.yaml
└── README.md
```

## 🚀 Deployment Steps
1. Clone this repository
2. Update the inventory file with your server IP:
   ```ini
   [cloud]
   your_server_ip ansible_user=root ansible_ssh_private_key_file=/path/to/your/key
   ```
3. Configure the environment variables in `app/.env`
4. Run the Ansible playbook:
   ```
   ansible-playbook -i ansible/inventory.ini ansible/main.yml
   ```

## 🐳 Docker Compose Configuration
The project deploys the following containers:
- **WordPress**: PHP and WordPress application
- **MySQL**: Database server
- **PHPMyAdmin**: Web interface for MySQL management
- **Nginx**: Reverse proxy with TLS support

## 🔧 Environment Variables
All sensitive information is stored in the `.env` file:
- `MYSQL_ROOT_PASSWORD`: Root password for MySQL
- `MYSQL_DATABASE`: WordPress database name
- `MYSQL_USER`: WordPress database user
- `MYSQL_PASSWORD`: WordPress database password
- `WORDPRESS_DB_HOST`: Database hostname
- `WORDPRESS_DB_NAME`: WordPress database name
- `WORDPRESS_DB_USER`: WordPress database user
- `WORDPRESS_DB_PASSWORD`: WordPress database password

## 🌐 Networking
- Web traffic is served on ports 80 (HTTP) and 443 (HTTPS)
- PHPMyAdmin is accessible through the web interface
- MySQL is not directly accessible from outside the Docker network

## 💾 Data Persistence
All data is stored in Docker volumes:
- WordPress files: `/var/www/html`
- MySQL database: `/var/lib/mysql`

## 🔄 Restart Policy
All containers are configured to restart automatically if the server reboots, ensuring continuous service availability.

## 🔒 Security Features
- MySQL is only accessible from within the Docker network
- TLS certificates for secure HTTPS connections
- Restricted access to sensitive services

## ❓ Troubleshooting
- Check container status: `docker ps`
- View container logs: `docker logs <container_name>`
- Restart a specific container: `docker restart <container_name>`
- Restart all containers: `docker-compose -f /app/docker-compose.yml restart`

## 📚 Resources
- [Ansible Documentation](https://docs.ansible.com/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [WordPress Documentation](https://wordpress.org/documentation/)
- [Nginx Documentation](https://nginx.org/en/docs/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PHPMyAdmin Documentation](https://www.phpmyadmin.net/docs/)
- [42 School Projects](https://42.fr/en/homepage/)

## 👏 Acknowledgements
- Based on the 42 school "Inception" project
- Leverages Ansible for automation
- Uses Docker and Docker Compose for containerization