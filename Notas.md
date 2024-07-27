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
sudo docker rm <NomeContêiner1> <NomeContêiner2> <etc...>
➜  sudo docker rm $(sudo docker ps -a -q) ## remove todos os containers
# NÃO pode remover um contêiner em execução --> causa erro


docker attach <containerID_Or_Name> ## ouvir o container --> ver as saidas dos outputs


docker logs <containerID_Or_Name> # ver os logs passados do container (outuputs passados )
docker logs -f <containerID_Or_Name> # ver os logs passados e os futuros (f - follow)



➜  docker run -i b8  # Faz com que seja possivel adicionar inputs exemplo do arquivo da aula 3 
➜  sudo docker run -it b8   # o -it faz com que o terminal do docker seja exposto para a gnt        --- adiciona inputs e outputs       

docker images  # Lista as imagens do docker

docker rmi d2c94e258dcb  # remove as imagens 


anahelena in Docker-Kubernetes on  main [!] 
➜  docker rmi b86551c2461f
Error response from daemon: conflict: unable to delete b86551c2461f (must be forced) - image is being used by stopped container 55fb2e390f16
anahelena in Docker-Kubernetes on  main [!] 
➜  docker rmi d2c94e258dcb            
Untagged: hello-world:latest
Untagged: hello-world@sha256:1408fec50309afee38f3535383f5b09419e6dc0925bc69891e79d84cc4cdcec6
Deleted: sha256:d2c94e258dcb3c5ac2798d32e1249e42ef01cba4841c2234249495f87264ac5a
Deleted: sha256:ac28800ec8bb38d5c35b49d45a6ac4777544941199075dff8c4eb63e093aa81e

docker image prune # remove todas as imagens que não estão sendo usadas por nenhum container parado ou em execução

anahelena in Docker-Kubernetes/Aula2/nodejs-app-starting-setup on  main [!] 
➜  docker image inspect 9f223
[
    {
        "Id": "sha256:9f223900b052f60301ca92f8c3d0729d8f73becd149a37febe307e5c0046e78e",
        "RepoTags": [],
        "RepoDigests": [],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2024-07-26T23:35:02.500876611-03:00",
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NODE_VERSION=22.5.1",
                "YARN_VERSION=1.22.22"
            ],
            "Cmd": [
                "node",
                "server.js"
            ],
            "ArgsEscaped": true,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "/app",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 1119145813,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/3mu183v2k1amwonsdqq5dges2/diff:/var/lib/docker/overlay2/04z2l2lshzcum9gvm8gbr3o9p/diff:/var/lib/docker/overlay2/61l8t30ml7hxjzaqeandhc9iv/diff:/var/lib/docker/overlay2/39870a467a4b3e1948c7e805312e44055e017bc7b3f30c8d2cb7a8e88ae29b22/diff:/var/lib/docker/overlay2/5ef33fbe243bb2de115b420a75a9941ca9cf12cfc9a9adf642618cd8cd6323c9/diff:/var/lib/docker/overlay2/f1843089c5107c3ae2d6c9941efbdc03f64275b4ac79afa604ee932418a345a3/diff:/var/lib/docker/overlay2/447e38220a7a99c39a6e50b165f4d3326e9ab38bbd2a1a3a12eb7b3b65cf4c93/diff:/var/lib/docker/overlay2/ffefc490d3081bc5c07dfd61e759deb41d04de6b4c1bcd713a95ee3e2158b551/diff:/var/lib/docker/overlay2/f0346d03d17293df5d7321d151b7db32774547914937f47026af8a150a2983e9/diff:/var/lib/docker/overlay2/d25202ef3f3840fd22450a3a5cf97539a57f177608d0f640045340e74ffea7e9/diff:/var/lib/docker/overlay2/5fc9956c538ea71a4f79d480c12c6c80bd3cfc2a420f161bb203426184e957d1/diff",
                "MergedDir": "/var/lib/docker/overlay2/9xwa66dnk9oe2b9s86kekzg8o/merged",
                "UpperDir": "/var/lib/docker/overlay2/9xwa66dnk9oe2b9s86kekzg8o/diff",
                "WorkDir": "/var/lib/docker/overlay2/9xwa66dnk9oe2b9s86kekzg8o/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:f6faf32734e0870d82ea890737958fe33ce9ddfed27b3b157576d2aadbab3322",
                "sha256:7cfafa82cfd2b6a92aeb90093e38fb88fa4377948d71bd970d11a51bae16d2f1",
                "sha256:0905150af928fc88e784dcad5ba98d5f3c2ab28c51c30ac7c7aa8599100cf02f",
                "sha256:ffe60aac26fce04aa507ee52ebf97f2da44fa5a2b475099d4260349c3e1cc329",
                "sha256:a0a8f41c2784069ce80bc1d189f2efc6cf76d00d7bc5edfb5468c06c5c54679c",
                "sha256:bcfeeb82a3a003b8d58e615fb5aa0613fc212dabb04150b9fe1bcdaecccee6da",
                "sha256:8f32fd06b28e54b08fdec4b8d6fbd25e82a5bab554351af4c3d5449e7d089a73",
                "sha256:9335ea658be8ff8f0bad9ab51573034c6e835b84e6b39b3565e7b983388b87ea",
                "sha256:fe3daa0449fdbc6077c8758c7ff0c1757296bd9ddaa0b36d6ba3cde5b05abf53",
                "sha256:a311c26f1001dff7f1caf6d55643d42e25c1033bf02c37ed8347e49b901b95f4",
                "sha256:bfc0981ccc0d184bcb78b0c59aecbde242bad23ea681d86caf0d527b677d5ce6",
                "sha256:31c2d9bbd4eea9c5de673882ba2a5fea90d6ddd510d8fc5ad433696cad1e58f0"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]


docker run --help 
            --rm # remove o contêiner quando sai de execução
docker run -p 3000:80 -d --rm 


























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
