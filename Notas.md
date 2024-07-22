# Comandos Docker
## Iniciais

```bash
sudo docker build . 
# retorna id da imagem


sudo docker run -p 3000:3000 5fc85f9debee7117a # id
#      porta conteiner X porta pc
docker ps -> ver conteiners

# retorno 

➜  sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS        PORTS                                       NAMES
5ce76b6b401b   5fc85f9debee   "docker-entrypoint.s…"   27 hours ago   Up 27 hours   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   wizardly_nash
47916ab60a27   5fc85f9debee   "docker-entrypoint.s…"   27 hours ago   Up 27 hours   3000/tcp                                    serene_faraday

sudo docker stop serene_faraday
```
#### Rodar docker do DockerHub

anahelena in Docker-Kubernetes/Aula 1first-demo-starting-setup/first-demo-starting-setup on  main [!?] 
➜  sudo docker run node
[sudo] senha para anahelena: 
Unable to find image 'node:latest' locally
latest: Pulling from library/node
fea1432adf09: Pull complete 
5651b5803b18: Pull complete 
3873416e6a33: Pull complete 
8a142b8b0e69: Pull complete 
23885ecc6bd0: Pull complete 
fc1dd23b13f8: Pull complete 
dfa6f8aa1b8e: Pull complete 
cdf8d5cb156d: Pull complete 
Digest: sha256:b98ec1c96103fbe1a9e449b3854bbc0a0ed1c5936882ae0939d4c3a771265b4b
Status: Downloaded newer image for node:latest

➜  sudo docker run -it node   # o -it faz com que o terminal do docker seja exposto para a gnt               
Welcome to Node.js v22.3.0.
Type ".help" for more information.
> 






























































# Dockerfile