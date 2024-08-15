## Removing Anonymous Volumes
We saw, that anonymous volumes are removed automatically, when a container is removed.

This happens when you start / run a container with the --rm option.

If you start a container without that option, the anonymous volume would NOT be removed, even if you remove the container (with docker rm ...).

Still, if you then re-create and re-run the container (i.e. you run docker run ... again), a new anonymous volume will be created. So even though the anonymous volume wasn't removed automatically, it'll also not be helpful because a different anonymous volume is attached the next time the container starts (i.e. you removed the old container and run a new one).

Now you just start piling up a bunch of unused anonymous volumes - you can clear them via docker volume rm VOL_NAME or docker volume prune.

Ver Arquivo do docker


https://headsigned.com/posts/mounting-docker-volumes-with-docker-toolbox-for-windows/


## Bind Mounts

```bash
anamarcacini in Docker-Kubernetes/Modulo2-Data&Volumes/Aula1 on  main [!] 
➜  docker run -d -p 3000:80 --rm -v feedback:/app/feedback -v "/home/anamarcacini/GIT/AnaMarcacini/Docker-Kubernetes/Modulo2-Data&Volumes/Aula1":/app feedback-node:volume
70fefda520b1d8c3ca5b081bb5231d6c770ae76f3ca043930555e87ee136af64

```

OBS quando coloco o caminho completo de uma pasta no dispositivo vira um volume do tipo Bind Mounts. Com isso a pasta anterior é sobrescrita e assim apaga as bibliotecas instaladas na imagem com o npm install dando esse problema



### Problema
```bash

➜  docker logs 8a626498d945c7d8e874dbc0f117c6386c2462b47cca9f99aaeba525e29345cb
internal/modules/cjs/loader.js:934
  throw err;
  ^

Error: Cannot find module 'express'
Require stack:
- /app/server.js
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:931:15)
    at Function.Module._load (internal/modules/cjs/loader.js:774:27)
    at Module.require (internal/modules/cjs/loader.js:1003:19)
    at require (internal/modules/cjs/helpers.js:107:18)
    at Object.<anonymous> (/app/server.js:5:17)
    at Module._compile (internal/modules/cjs/loader.js:1114:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1143:10)
    at Module.load (internal/modules/cjs/loader.js:979:32)
    at Function.Module._load (internal/modules/cjs/loader.js:819:12)
    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:75:12) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [ '/app/server.js' ]
}
```
Eu posso criar um repositorio não nomeado (anonimo) para armazenar os dados que eu sobrescreveria e dessa forma não irei perder esses dados

---> -v /app/node_modules equivalente à fazer  VOLUME [ "/app/feedback" ] no dockerfile | cria um volume anonimo

➜  docker run -d -p 3000:80 -v feedback:/app/feedback -v "/home/anamarcacini/GIT/AnaMarcacini/Docker-Kubernetes/Modulo2-Data&Volumes/Aula1":/app -v /app/node_modules feedback-node:volume


Os caminhos mais especificos sobrescrevem os menos --> no caso o  /app/node_modules ganha do /app


  docker inspect b59b1943dfbea1f0714ab109a87c591026f28dea16f5ee43dc2524312e01547c
......
   "Mounts": [
            {
                "Type": "volume",
                "Name": "feedback",
                "Source": "/var/lib/docker/volumes/feedback/_data",
                "Destination": "/app/feedback",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            },
            {
                "Type": "bind",
                "Source": "/home/anamarcacini/GIT/AnaMarcacini/Docker-Kubernetes/Modulo2-Data&Volumes/Aula1",
                "Destination": "/app",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "volume",
                "Name": "56eff9954616bc4c8cdeee78b4c230764fbf6dedae748e8cdd6587cc773076c9",
                "Source": "/var/lib/docker/volumes/56eff9954616bc4c8cdeee78b4c230764fbf6dedae748e8cdd6587cc773076c9/_data",
                "Destination": "/app/node_modules",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],

......
