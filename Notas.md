# Comandos Docker
## Iniciais

```bash
docker --help

sudo docker build . 
# retorna id da imagem


sudo docker run -p 3000:3000 5fc85f9debee7117a # id
#      porta conteiner X porta pc
sudo docker run -p 3000:3000 -d 5fc85f9debee7117a # id
#retorna o id do container e sai do attached mode (não fica preso no terminal do container) || d = detached mode
docker ps #-> ver containers || listar todos os containers

# retorno 

➜  sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS        PORTS                                       NAMES
5ce76b6b401b   5fc85f9debee   "docker-entrypoint.s…"   27 hours ago   Up 27 hours   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   wizardly_nash
47916ab60a27   5fc85f9debee   "docker-entrypoint.s…"   27 hours ago   Up 27 hours   3000/tcp                                    serene_faraday


➜  sudo docker ps -a # Ver todos os containers que vc tinha no passado incluindo os que não estão em execução

anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!?] took 4,8s 
➜  sudo docker ps -a
[sudo] senha para anahelena: 
CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS                           PORTS                                   NAMES
cac97337c799   b571dea73f82   "docker-entrypoint.s…"   31 minutes ago      Up 31 minutes                    0.0.0.0:3000->80/tcp, :::3000->80/tcp   wizardly_goldberg
1bd5b81f8de0   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Exited (137) 49 minutes ago                                              objective_driscoll
b22f189c5803   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Created                                                                  cool_wozniak
8d07861f30d8   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Exited (137) About an hour ago                                           determined_carver
26b337f944e6   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Created                                                                  reverent_ramanujan
c08364acd474   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Created                                                                  stoic_swartz
f2de3a6851d8   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Created                                                                  xenodochial_maxwell
d6249e5545fb   528a3f32586b   "docker-entrypoint.s…"   About an hour ago   Exited (137) About an hour ago                                           infallible_saha
0884f6033e57   hello-world    "/hello"                 4 days ago          Exited (0) 4 days ago                                                    blissful_snyder
b6859f84009e   hello-world    "/hello"                 4 days ago          Exited (0) 4 days ago                                                    elated_hodgk

sudo docker stop serene_faraday # para a execução do container
➜  docker stop $(docker ps -q) # Para todos os containers
docker start CONTAINER_NAME # executa um container já criado || que foi parado
docker start -a CONTAINER_NAME # executa um container já criado e faz attach (fica ouvindo os seus logs no terminal) NÃO PERMITE INPUTS
docker start -a -i CONTAINER_NAME # executa um container já criado e faz attach (fica ouvindo os seus logs no terminal) E PERMITE INPUTS

➜  sudo docker rm $(sudo docker ps -a -q) ## remove todos os containers



docker attach <containerID_Or_Name> ## ouvir o container --> ver as saidas dos outputs


docker logs <containerID_Or_Name> # ver os logs passados do container (outuputs passados )
docker logs -f <containerID_Or_Name> # ver os logs passados e os futuros (f - follow)

```
#### Rodar docker do DockerHub
```bash

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


➜  docker run -i b8  # Faz com que seja possivel adicionar inputs exemplo do arquivo da aula 3 
➜  sudo docker run -it b8   # o -it faz com que o terminal do docker seja exposto para a gnt        --- adiciona inputs e outputs       


```


## Docker ps


```bash

anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!?] took 2,7s 
➜  sudo docker ps --help

Usage:  docker ps [OPTIONS]

List containers

Aliases:
  docker container ls, docker container list, docker container ps, docker ps

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Format output using a custom template:
                        'table':            Print output in table format with column headers (default)
                        'table TEMPLATE':   Print output in table format using the given Go template
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using the given Go template.
                        Refer to https://docs.docker.com/go/formatting/ for more information about formatting output with templates
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display container IDs
  -s, --size            Display total file sizes

```


















































# Dockerfile

## Comandos 
















## Teoria

### layers (camadas)
```dockerfile
FROM node                       # camadas superiores 
WORKDIR /app 
COPY . ./
RUN npm i
EXPOSE 80
CMD ["node", "server.js"]       # Camadas inferiores 
```


O docker possui um cache que faz com que a criação ou realização de comandos iguais seja armazenados em cache. Assim a construção (docker build .) de imagens e comandos iguais será realizado de forma mais rápida. 
Porém caso o docker perseba uma alteração nas camadas superiores altera todas as camadas inferiores a ela. Assim se o código copiado em copy ./app for alterado ou for adicionado novos comandos todos os coamandos das camadas a baixo serão alterados 

Assim a melhor estrategia é deixar o código fonte em uma camada inferior para não precisar executar novamente o npm i
```dockerfile
FROM node 
WORKDIR /app 
COPY package.json /app 
RUN npm i
COPY . /app 
EXPOSE 80
CMD ["node", "server.js"]

```

```bash
anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!?] took 4,0s 
➜  sudo docker build . 
[+] Building 0.7s (10/10) FINISHED                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile
 => => transferring dockerfile: 1.12kB                       
 => [internal] load metadata for docker.io/library/node:latest                                                                                                         
 => [internal] load .dockerignore                                                                                                          
 => => transferring context: 2B                                                                                                                    
 => [1/5] FROM docker.io/library/node:latest@sha256:d885885ad8e100d27b65e7837075afea042cc8515ec066cd82cdf34e26fc9fb8                                   
 => [internal] load build context                                                                                                               
 => => transferring context: 319B                                                                                                                  
 => CACHED [2/5] WORKDIR /app                                                                                                                   
 => CACHED [3/5] COPY package.json /app                                                                                                                   
 => CACHED [4/5] RUN npm i                                                                                                                     
 => CACHED [5/5] COPY . /app                                                                                                                   
 => exporting to image                                                                                                                 
 => => exporting layers                                                                                                                
 => => writing image sha256:b09d780306980df437c641badc093d479f7c2386b458e6b92bf079bc070345cd

anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!?] 
➜  sudo docker build . 
[+] Building 0.8s (10/10) FINISHED                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                               
 => => transferring dockerfile: 1.12kB                                                                                                                                  
 => [internal] load metadata for docker.io/library/node:latest                                                                                                          
 => [internal] load .dockerignore                                                                                                         
 => => transferring context: 2B                                                                                                                   
 => [internal] load build context                                                                                                              
 => => transferring context: 1.27kB                                                                                                                 
 => [1/5] FROM docker.io/library/node:latest@sha256:d885885ad8e100d27b65e7837075afea042cc8515ec066cd82cdf34e26fc9fb8                                  
 => CACHED [2/5] WORKDIR /app                                                                                                                  
 => CACHED [3/5] COPY package.json /app                                                                                                                  
 => CACHED [4/5] RUN npm i                                                                                                                    
 => [5/5] COPY . /app                                                                                                                  
 => exporting to image                                                                                                                
 => => exporting layers                                                                                                               
 => => writing image sha256:b571dea73f826d027f8ab9ec0081efd2f783d6dc125f4076e139c6bbec1bb9a2
```
