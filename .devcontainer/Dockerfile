FROM node:latest

# Usa root para configurar o ambiente
USER root

# Atualiza pacotes e instala sudo
RUN apt-get update && apt-get install -y sudo

# Adiciona o usuário "node" ao grupo sudo
RUN adduser node sudo

# Permite que o usuário node use sudo sem senha
RUN echo "node ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Cria o diretório de trabalho e dá permissões ao usuário node
RUN mkdir -p /workspace && chown -R node:node /workspace

# Define diretório de trabalho
WORKDIR /workspace

# Instala Angular CLI globalmente como root
RUN npm install -g @angular/cli@14.2.0

# Muda para o usuário node para garantir permissões
USER node

# Copia os arquivos do projeto e instala dependências
COPY --chown=node:node package*.json ./
RUN npm install

COPY --chown=node:node . .

# Expõe a porta do Angular
EXPOSE 4200

# Comando default para rodar o servidor Angular
CMD ["ng", "serve", "--host", "0.0.0.0", "--poll=2000"]
