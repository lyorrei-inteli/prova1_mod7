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