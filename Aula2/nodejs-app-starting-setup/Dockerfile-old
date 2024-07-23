FROM node 
# procura uma imagem com esse nome no docker hub ou local 
# no caso como já rodei essa imagem no meu computador local e ela já foi baixada ele vai pegar a imagem local

# Quais arquivos vão ser copiados para o conteiner

# COPY . /app
# # fora do conteiner (pasta do dockerfile) X dentro do conteiner (é criada se necessário)

WORKDIR /app 
# diretorio onde vou rodar os comandos


COPY . ./
# COPY . /app # também pode usar o caminho completo (absoluto) || eu acho preferivel

RUN npm i

# expõe a porta 80 do conteiner
EXPOSE 80

## esse comando CMD roda não quando instancia uma imagem mas sim quando o conteiner for iniciado 
CMD ["node", "server.js"]

# sudo docker run -p 3000:80 f9ce8db7032fc642a