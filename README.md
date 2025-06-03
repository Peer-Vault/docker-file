# Peer Vault - Docker Compose Setup

## 🚀 Overview
This repository contains Docker Compose configurations to quickly set up essential infrastructure services for the Peer Vault microservices ecosystem. It provides ready-to-use configurations for your **MySQL database** and **Apache Kafka** (with Zookeeper and Schema Registry), enabling a consistent development and deployment environment.

---

## ✨ Features
* **MySQL Database:** Provides a persistent MySQL 8.x database instance for data storage.
* **Apache Kafka:** Sets up a Kafka broker along with Zookeeper for coordination and Schema Registry for schema management, crucial for asynchronous communication between microservices.
* **Containerized Environment:** All services run in isolated Docker containers, ensuring environment consistency and easy setup.
* **Volume Mounting:** Persistent volumes are configured for data and logs, preventing data loss across container restarts.

---

## 🛠 Tech Stack
* Docker
* Docker Compose
* MySQL 8.x
* Apache Kafka (Confluent Platform images)
* Apache Zookeeper
* Confluent Schema Registry

---

## 🏗 Installation & Setup

### Prerequisites
* **Docker Desktop** (or Docker Engine and Docker Compose) installed on your system.

### Configuration

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/Peer-Vault/docker-file.git
    cd docker-file
    ```

2.  **Database Configuration (`db` service):**
    * **MySQL Root Password:** The `MYSQL_ROOT_PASSWORD` is set to `root` by default. You can change this in the `docker-compose.yml` file.
    * **MySQL Configuration:** A custom `my.cnf` file is mounted from `./config/mysql/my.cnf`. Ensure this file exists and contains any specific MySQL configurations you need.
    * **Data and Logs:** Data will be persisted in `./data` and logs in `./logs/mysql` on your host machine.

3.  **Kafka Configuration (`zookeeper`, `kafka`, `schema-registry` services):**
    * **Network:** These services run on a custom `kafka_network` to ensure proper inter-service communication within Docker.
    * **Ports:**
        * Zookeeper: `2181`
        * Kafka: `9092` (internal) and `29092` (external for host access)
        * Schema Registry: `8081`
    * **Volumes:** Data for Zookeeper and Kafka is persisted in `./zookeeper/data/zookeeper`, `./zookeeper/logs/zookeeper`, and `./kafka/data` respectively.

### Running the Services

1.  **Start all services:**
    Navigate to the cloned `docker-file` directory and run:
    ```bash
    docker-compose up -d
    ```
    The `-d` flag runs the containers in detached mode (in the background).

2.  **Verify services are running:**
    ```bash
    docker-compose ps
    ```
    You should see `mysql8`, `zookeeper`, `kafka`, and `schema-registry` containers in a `Up` state.

3.  **Stop the services:**
    ```bash
    docker-compose down
    ```
    This will stop and remove the containers, but keep the volumes (data) by default.

4.  **Stop and remove services and volumes (clean-up):**
    ```bash
    docker-compose down -v
    ```
    This will stop and remove containers, networks, and all named volumes. Use with caution as it will delete your MySQL and Kafka data.

---

## 🎯 Usage
Once these infrastructure services are running, your Peer Vault microservices can connect to them:

* **MySQL Connection:** Connect to `localhost:3306` (assuming `network_mode: host` is used for `db` or `host.docker.internal` from other containers).
* **Kafka Broker:** Connect to `localhost:29092` from your host machine or `kafka:9092` from other Docker containers within the `kafka_network`.
* **Zookeeper:** Accessible on `localhost:2181`.
* **Schema Registry:** Accessible on `localhost:8081`.

These services form the backbone for data persistence and asynchronous communication for your Peer Vault applications.

---

## 🤝 Contributing
Contributions and suggestions are welcome! Feel free to open issues or submit pull requests to improve these Docker Compose configurations.

 
---

## 👨‍💻 Author
Developed and maintained by the Peer Vault team.

---

🌟 Star this repo if you find it helpful! 🌟
