# Programowanie aplikacji w chmurze obliczeniowej - Laboratorium 11
## 1. Utworzenie sieci mostkowej
Nie podając `--driver bridge` docker domyślnie utworzy sieć mostkową 
```bash
docker network create lab11net
```
![network create](img/network_create.png)
## 2. Uruchomienie kontenerów z nginx i podłączenie wolumenów
Dodając `:ro` na końcu ścieżki docelowej wolumenu ustawiamy go w tryb read-only
```bash
docker run -d --name web1 --network lab11net -p 8081:80 -v C:/Users/iver3/lab11/web1/html:/usr/share/nginx/html:ro -v C:/Users/iver3/lab11/web1/logs:/var/log/nginx nginx:latest
docker run -d --name web2 --network lab11net -p 8082:80 -v C:/Users/iver3/lab11/web2/html:/usr/share/nginx/html:ro -v C:/Users/iver3/lab11/web2/logs:/var/log/nginx nginx:latest
docker run -d --name web3 --network lab11net -p 8083:80 -v C:/Users/iver3/lab11/web3/html:/usr/share/nginx/html:ro -v C:/Users/iver3/lab11/web3/logs:/var/log/nginx nginx:latest
```
![Docker run](img/docker_run.png)
## 3. Potwierdzenie uruchomienia kontenerów
```bash
docker ps
```
![Docker ps](img/docker_ps.png)
## 4. Potwierdzenie działania kontenerów w sieci lab11net
```bash
docker network inspect lab11net
```
![network inspect](img/network_inspect.png)
## 5. Potwierdzenie poprawnego nadania uprawnień dla wolumenów
```bash
docker container inspect web1
docker container inspect web2
docker container inspect web3 
```
![Docker container inspect 1](img/container_inspect1.png)
![Docker container inspect 2](img/container_inspect2.png)
![Docker container inspect 3](img/container_inspect4.png)
## 6. Potwierdzenie poprawnego działania aplikacji
```bash
curl http://localhost:8081
curl http://localhost:8082
curl http://localhost:8083
```
![curl 1](img/curl1.png)
![curl 2](img/curl2.png)
![curl 3](img/curl3.png)
## 7. Sprawdzenie logów z maszyny macierzystej
```bash
ls ~/lab11/web1/logs
ls ~/lab11/web2/logs
ls ~/lab11/web3/logs

cat ~/lab11/web1/logs/access.log
```
![ls logs](img/logs.png)
![cat](img/access.png)
