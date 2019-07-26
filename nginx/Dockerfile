FROM node:10-alpine as build-deps

RUN mkdir -p /usr/src/app/front-end
WORKDIR /app/front-end

# Apesar do processo de build ficar mais lento
# eu prefiro instalar a pasta "node_modules" 
# dinamicamente dentro do container. Pode-se tb
# usar o npm install localmente e depois copiar
# a node_modules, mas o risco de incompatibilidade
# entre versoes de Node.JS é grande, se quiser 
# utilizar esse metodo, recomendo uso do NVM. 
# ref: https://github.com/nvm-sh/nvm

COPY front-end/package.json /app/front-end/
RUN npm install

# Em produção essa linha é sem comentários
# COPY front-end /app/front-end/
# RUN npm run build

FROM nginx:alpine

COPY nginx/dev.conf /etc/nginx/nginx.conf
COPY --from=build-deps /app/front-end/dist/ /dist/

CMD ["nginx", "-g", "daemon off;"]
