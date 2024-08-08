#  Base image
FROM node:14 
# Entrar nesse diretorio
WORKDIR /app
# copiar o arquivo json
COPY package.json .
# rodar no terminal
RUN npm install
# copia o resto do codigo
COPY . .
# expor a porta 3000 para o mundo externo
EXPOSE 3000
# executa app.js com o comando node 
CMD [ "node", "app.mjs" ]