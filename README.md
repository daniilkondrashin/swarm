## Инициализация Docker Swarm
```sh
docker swarm init --advertise-addr <Ваш_Приватный_IP>
```
## Добавление worker-узла
```sh
docker swarm join --token <TOKEN> <Ваш_Приватный_IP>:2377
```
## Создание сети для traefik
```sh
docker network create --driver=overlay traefik-public
```
## Создание тега на узле
```sh
export NODE_ID=$(docker info -f '{{.Swarm.NodeID}}')

docker node update --label-add traefik-public.traefik-public-certificates=true $NODE_ID
```
## Запуск traefik
```sh
docker stack deploy -c compose.yaml traefik
```
## Запуск app
```sh
docker stack deploy -c compose.yaml whoami

```
