FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

CMD [ "node", "server.js" ]

# docker build -t feedback-node .
# ➜  docker run -p 3000:80 -d --name feedback-app --rm feedback-node:latest
# http://localhost:3000/