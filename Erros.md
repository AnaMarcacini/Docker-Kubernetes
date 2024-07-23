## Aula 1
```bash
anahelena in Docker-Kubernetes on  main [!?] 
➜  docker build .                            
ERROR: Cannot connect to the Docker daemon at unix:///home/anahelena/.docker/desktop/docker.sock. Is the docker daemon running?
anahelena in Docker-Kubernetes on  main [!?] 
➜  export DOCKER_HOST=unix:///run/docker.sock
anahelena in Docker-Kubernetes on  main [!?] 
➜  docker build .                            
ERROR: permission denied while trying to connect to the Docker daemon socket at unix:///run/docker.sock: Get "http://%2Frun%2Fdocker.sock/_ping": dial unix /run/docker.sock: connect: permission denied
anahelena in Docker-Kubernetes on  main [!?] 
➜  sudo !! 
anahelena in Docker-Kubernetes on  main [!?] 
➜  sudo docker build .
[sudo] senha para anahelena: 
[+] Building 0.1s (1/1) FINISHED                                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                  0.0s
 => => transferring dockerfile: 2B                                                                                                                                                    0.0s
ERROR: failed to solve: failed to read dockerfile: open Dockerfile: no such file or directory
anahelena in Docker-Kubernetes on  main [!?] took 5,0s 
```



```bash
# Outras tentativas
sudo systemctl start docker
sudo systemctl restart docker
sudo usermod -aG docker $USER
# Possivel tentativa

sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get install docker-ce docker-ce-cli containerd.io

```


## Aula 2
```bash

anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!?] 
➜  sudo docker stop *                 
Error response from daemon: No such container: 3f54de98-f75e-41a7-b209-5ce09ea2f517_EXPOSE__A_Little_Utility_Functionality.pdf
Error response from daemon: No such container: Dockerfile
Error response from daemon: No such container: Dockerfile-old
Error response from daemon: No such container: package.json
Error response from daemon: No such container: public
Error response from daemon: No such container: server.js

```


## Aula 4
```bash
sudo usermod -aG docker $USER # Adicionar seu usuário ao grupo docker
su - $USER # reinicie a sessão

sudo chmod 666 /var/run/docker.sock ## permissões do socket do Docker

sudo systemctl restart docker # reinicie

export DOCKER_HOST=unix:///var/run/docker.sock # Verifique se o Docker está usando o socket correto







```