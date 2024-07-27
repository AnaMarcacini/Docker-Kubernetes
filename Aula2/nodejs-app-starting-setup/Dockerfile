FROM node:12
#  name : tag
# procura uma imagem com esse nome no docker hub ou local 
# no caso como já rodei essa imagem no meu computador local e ela já foi baixada ele vai pegar a imagem local

# Quais arquivos vão ser copiados para o conteiner

# COPY . /app
# # fora do conteiner (pasta do dockerfile) X dentro do conteiner (é criada se necessário)

WORKDIR /app 
# diretorio onde vou rodar os comandos


COPY package.json /app 

# usando o caminho completo (absoluto) || eu preferivel

RUN npm i

COPY . /app 
# evita que a cada alteração na aplicação o conteiner tenha que reinstalar tudo de novo em sua construção 
# Agora que o camado do comando copy está abaixo da npm i uma alteração nele apenas interferirá nos comandos a baixo do copy
# porém caso o package json seja atualizado deverá reinstalar as dependencias por isso esse arquivo foi importado antes

# expõe a porta 80 do conteiner
EXPOSE 80

## esse comando CMD roda não quando instancia uma imagem mas sim quando o conteiner for iniciado 
CMD ["node", "server.js"]

# sudo docker run -p 3000:80 f9ce8db7032fc642a