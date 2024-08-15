FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80
# adicionando um volume anonimo 
VOLUME [ "/app/feedback" ] 
# o docker salva em algum lugar do seu pc e vc nn sabe onde 
# listando os volumes 
# docker volume ls
#  quando para o container para de listar -- ele só existe enquanto o container existir
CMD [ "node", "server.js" ]

# docker build -t feedback-node .
# ➜  docker run -p 3000:80 -d --name feedback-app --rm feedback-node:latest
# http://localhost:3000/