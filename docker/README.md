
```bash
docker build -t urban-traffic-management-app:latest --file ./urban-traffic-management/docker/Dockerfile .
docker images
docker rmi --force $(docker images | grep "^<none>" | awk '{print $3}') 
docker run --name urban-traffic-management-app -it --rm -p 7200:7200/tcp urban-traffic-management-app:latest
docker ps
docker exec -it urban-traffic-management-app sh
docker exec -it urban-traffic-management-app sh -c "cat /opt/urbanboot/urban-traffic-management/logs/access.log"
docker rm $(docker ps -a -q)

# 使用 docker-compose
docker-compose -f ./docker/docker-compose.yaml up
docker-compose -f ./docker/docker-compose.yaml down
```
