

```
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] took 38,1s 
➜  docker run feedback-node:latest 
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] took 37,4s 
➜  docker run -p 3000:80 -d --name feedback-app --rm feedback-node:latest
8b7623929704d9d3aa3031f0cb9d31560f5048e9251761830c93955ebc0a9afa
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] 
➜  docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                                   NAMES
8b7623929704   feedback-node:latest   "docker-entrypoint.s…"   6 seconds ago   Up 6 seconds   0.0.0.0:3000->80/tcp, :::3000->80/tcp   feedback-app
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] 
➜  docker stop 8b7623929704 
8b7623929704
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] took 10,4s 
➜  docker run -p 3000:80 -d --name feedback-app feedback-node:latest     
e56046b58dd7731de4c82f92d4d747cec2e80d131e5c53c1cad2ebb26139ac4a
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [?] 
```



# Volumes

Pastas da maquina host (seu computador) que estão montados os arquivos do container





