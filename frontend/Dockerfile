# Utiliza a imagem oficial do Node.js como base
FROM node:lts

# Estabelece o diretório de trabalho
WORKDIR /usr/src/app

# Copia o arquivo que contém as dependências utilizadas no projeto
COPY package*.json ./

# Instala as dependências
RUN npm install

# Copia o restante dos arquivos do projeto
COPY . .

# Expõe a porta da aplicação
EXPOSE 3000

# Comando que inicia o servidor
CMD ["node", "server.js"]