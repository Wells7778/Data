# Local Database Setup Using Docker Compose

## Project Overview

This project provides a Docker Compose setup for local development with various databases, including MongoDB, MariaDB, MySQL (multiple versions), Redis, Elasticsearch, Kibana, and PostgreSQL. The goal is to allow developers to quickly spin up these databases in their local environment for development and testing purposes.

## Prerequisites

- Docker
- Docker Compose
- Sufficient disk space for storing database files locally

## Services and Databases

1. **MongoDB** (`mongo`):
   - **Image**: `mongo`
   - **Authentication**: Enabled with `weiby` as the root user.
   - **Data Storage**: `./data/mongo/db:/data/db`
   - **Port**: `27017`
   - **Healthcheck**: Monitors the MongoDB server's status.

2. **MySQL 8** (`main`):
   - **Image**: `mysql:8`
   - **Port**: `3306`
   - **Time Zone**: `Asia/Taipei`
   - **Data Storage**: `./data/mysql/8:/var/lib/mysql`
   - **Healthcheck**: Pings the server for readiness.

3. **MySQL 5.7** (`mysql57`):
   - **Image**: `mysql:5.7`
   - **Port**: `3307`
   - **Time Zone**: `Asia/Taipei`
   - **Data Storage**: `./data/mysql/5.7:/var/lib/mysql`
   - **Healthcheck**: Pings the server for readiness.

4. **MariaDB** (`mariadb`):
   - **Image**: `mariadb:10.11.7`
   - **Port**: `3308`
   - **Time Zone**: `Asia/Taipei`
   - **Data Storage**: `./data/mariadb:/var/lib/mysql`
   - **Healthcheck**: Pings the server for readiness.

5. **Redis** (`redis`):
   - **Image**: `redis`
   - **Data Storage**: `./data/redis/data:/data`

6. **Elasticsearch** (`elasticsearch`):
   - **Image**: Custom-built from `Dockerfile.elasticsearch`
   - **Ports**: `9200`, `9300`
   - **Data Storage**: `./data/elasticsearch/esdata:/usr/share/elasticsearch/data`
   - **Memory**: Allocated 512MB for heap space.

7. **Kibana** (`kibana`):
   - **Image**: `docker.elastic.co/kibana/kibana:7.14.1`
   - **Port**: `5601`

8. **PostgreSQL** (`postgresql`):
   - **Image**: `postgres`
   - **Port**: `5432`
   - **Time Zone**: `Asia/Taipei`
   - **Data Storage**: `./data/postgresql/data:/var/lib/postgresql/data`
   - **Healthcheck**: Uses `pg_isready` to check the server's readiness.

## Usage

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <project-directory>
```

### 2. Start Services
To bring up all services:

```bash
docker-compose up -d <service_name>
```

### 3. Accessing Databases
- MongoDB: Connect on mongodb://weiby:password@localhost:27017
- MariaDB: Access on port 3308
- MySQL 8: Access on port 3306
- MySQL 5.7: Access on port 3307
- Redis: Access on localhost:6379
- Elasticsearch: Access on localhost:9200
- Kibana: Open http://localhost:5601
- PostgreSQL: Access on port 5432

### 4. Stopping the Services

```bash
docker-compose down
```

## Volumes and Data Persistence
The data for each service is persisted in the ./data directory under the project folder. Each service has its respective subfolder for data storage:

- ./data/mongo/db
- ./data/mariadb
- ./data/mysql/8
- ./data/mysql/5.7
- ./data/redis/data
- ./data/elasticsearch/esdata
- ./data/postgresql/data

## Health Checks
Each service is equipped with a health check to ensure they are up and running properly. If any service fails its health check, Docker Compose will attempt to restart it according to the restart: always policy.

## Networks
All services are connected through a custom Docker network (db_network) with the following

---


# 使用 Docker Compose 建立本地資料庫環境

## 專案概述

此專案提供一個 Docker Compose 設定，供開發人員在本地開發環境中快速啟動多種資料庫，包括 MongoDB、MariaDB、MySQL（多個版本）、Redis、Elasticsearch、Kibana 和 PostgreSQL。目的是讓開發人員能夠快速建立這些資料庫，用於開發和測試。

## 先決條件

- Docker
- Docker Compose
- 充足的磁碟空間以存儲資料庫文件

## 服務與資料庫

1. **MongoDB** (`mongo`):
   - **映像檔**: `mongo`
   - **資料存儲**: `./data/mongo/db:/data/db`
   - **連接埠**: `27017`
   - **健康檢查**: 監控 MongoDB 伺服器的狀態。

2. **MySQL 8** (`main`):
   - **映像檔**: `mysql:8`
   - **連接埠**: `3306`
   - **時區**: `Asia/Taipei`
   - **資料存儲**: `./data/mysql/8:/var/lib/mysql`
   - **健康檢查**: Ping 測試伺服器是否可用。

3. **MySQL 5.7** (`mysql57`):
   - **映像檔**: `mysql:5.7`
   - **連接埠**: `3307`
   - **時區**: `Asia/Taipei`
   - **資料存儲**: `./data/mysql/5.7:/var/lib/mysql`
   - **健康檢查**: Ping 測試伺服器是否可用。

4. **MariaDB** (`mariadb`):
   - **映像檔**: `mariadb:10.11.7`
   - **連接埠**: `3308`
   - **時區**: `Asia/Taipei`
   - **資料存儲**: `./data/mariadb:/var/lib/mysql`
   - **健康檢查**: Ping 測試伺服器是否可用。

5. **Redis** (`redis`):
   - **映像檔**: `redis`
   - **資料存儲**: `./data/redis/data:/data`

6. **Elasticsearch** (`elasticsearch`):
   - **映像檔**: 由 `Dockerfile.elasticsearch` 自定義構建
   - **連接埠**: `9200`, `9300`
   - **資料存儲**: `./data/elasticsearch/esdata:/usr/share/elasticsearch/data`
   - **記憶體**: 分配 512MB 作為堆積空間。

7. **Kibana** (`kibana`):
   - **映像檔**: `docker.elastic.co/kibana/kibana:7.14.1`
   - **連接埠**: `5601`

8. **PostgreSQL** (`postgresql`):
   - **映像檔**: `postgres`
   - **連接埠**: `5432`
   - **時區**: `Asia/Taipei`
   - **資料存儲**: `./data/postgresql/data:/var/lib/postgresql/data`
   - **健康檢查**: 使用 `pg_isready` 檢查伺服器狀態。

## 使用方法

### 1. 下載專案

```bash
git clone <repository-url>
cd <project-directory>
```

### 2. 啟動服務
要啟動所有服務:

```bash
docker-compose up -d
```

啟用特定服務: (例: 只需要mongo和mysql 8.0)

```bash
docker-compose up -d mysql mongo
```

### 3. 停止服務

```bash
docker-compose down
```

### 資料儲存
每個服務的資料都會持久化存儲在專案資料夾中的 ./data 目錄下。每個服務對應一個子資料夾來存儲資料：

- ./data/mongo/db
- ./data/mariadb
- ./data/mysql/8
- ./data/mysql/5.7
- ./data/redis/data
- ./data/elasticsearch/esdata
- ./data/postgresql/data

### 網路
所有服務都連接到自定義 Docker 網路 (db_network)