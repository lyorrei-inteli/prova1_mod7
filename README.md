# Prova 1 Módulo 7

O projeto consiste em um CRUD de usuários.

## 📂 Estrutura de Pastas

O projeto está dividido em duas partes principais: o backend e o frontend. Abaixo está uma visão geral da organização e estrutura das pastas:

```
📦 Project
 ┣ 📂 backend               # Pasta raiz do backend 
 ┃ ┗ 📜 main.py             # Ponto de entrada da api 
 ┃ ┗ 📜 Dockerfile          # Arquivo docker com instruções para construir o container do backend
 ┣ 📂 frontend              # Pasta raiz do frontend 
 ┃ ┗ 📜 index.html          # Arquivo frontend
 ┃ ┗ 📜 Dockerfile          # Arquivo docker com instruções para construir o container do frontend
 ┗ 📜 README.md             # Descrição e documentação do projeto
 ┗ 📜 docker-compose.yml    # Arquivo docker para a utilização de múltiplos containers
```

## 🚀 Instalação e Uso

### Pré-requisitos

- Docker
- Docker Compose

### Configuração e Inicialização

Com o terminal na pasta root do projeto, construa e inicie os containers:
```bash
docker compose up
```

O backend estará rodando em `http://localhost:8000`, o frontend em `http://localhost:3000`.

Para parar os containers, use:

```bash
docker compose down -v
```

### Docker hub images 
#### Backend
Link para a imagem do backend: <a href="https://hub.docker.com/repository/docker/lyorrei/prova1-mod7-backend/general">Clique aqui</a>

Link completo para o backend: https://hub.docker.com/repository/docker/lyorrei/prova1-mod7-backend/general

#### Frontend
Link para a imagem do frontend: <a href="https://hub.docker.com/repository/docker/lyorrei/prova1-mod7-frontend/general">Clique aqui</a>

Link completo para o frontend: https://hub.docker.com/repository/docker/lyorrei/prova1-mod7-frontend/general

### Justificativa para cada linha dos Dockerfiles e docker-compose

#### Backend (Dockerfile)
```
# Utiliza a imagem oficial do Python:3.11 como base
FROM python:3.11.2-alpine3.17

# Estabelece o diretório de trabalho dentro do container
WORKDIR /usr/src/app

# Copia o arquivo que contém as dependências utilizadas no projeto
COPY requirements.txt .

# Instala as dependências
RUN pip install --no-cache-dir -r requirements.txt

# Copia o restante dos arquivos do projeto
COPY . .

# Expõe a porta da aplicação
EXPOSE 8000

# Comando que inicia o servidor
CMD ["python", "main.py"]
```

#### Frontend (Dockerfile)
```
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
```

#### Docker compose
```
# Estabelece que queremos utilizar a versão 3 do docker
version: '3'

# Serviços da nossa aplicação (backend e frontend)
services:
  backend:
    # Linha que aponta para o dockerfile do backend
    build: $PWD/backend

    # Estabelece que se acontecer algum problema ao rodar a aplicação, o docker tentará rodá-la novamente (mais uma medida de segurança)
    restart: always

    # Bind das portas do nosso computador com as de dentro do container
    ports:
      - "8000:8000"

  frontend:
    # Linha que aponta para o dockerfile do frontend
    build: $PWD/frontend

    # Estabelece que se acontecer algum problema ao rodar a aplicação, o docker tentará rodá-la novamente (mais uma medida de segurança)
    restart: always

    # Bind das portas do nosso computador com as de dentro do container
    ports:
      - "3000:3000"

    # Linha que diz que o container do frontend deve ser ligado após o container do backend (visto que o frontend depende do backend para funcionar)
    depends_on:
      - backend
```