# Networks
#### To establish communication between two containers

### Type of Network
- host
- bridge
- user defined bridge
- none

```
docker network ls       # List Network
docker network create two-tier -d bridge        # Create netwrok, -d: Driver
```
# Volumes
#### To persist data
```
docker volume create mysql-data
```
```
docker volume ls
```
- mountpoint: `/var/lib/docker/volumes/mysql_data/_data`

#### MYSQL Container
```
docker run -d --name mysql \
--network two-tier \
-v mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DB=devops \
mysql

```
- Make Image : 
```
docker build -t flask-backend .
```
#### Two-Tier Flask Backend Container
```
docker run -d --name two-tier-backend \
-p 5000:5000
--network two-tier \
-e MYSQL_HOST=mysql
-e MYSQL_USER=root \
-e MYSQL_PASSWORD=root \
-e MYSQL_DB=devops \
flask-backend
```
# Docker Compose
#### It is use to make one or more container at a time.
```
docker compose up --build -d
```