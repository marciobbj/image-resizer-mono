FROM node:11 as build-deps

WORKDIR /app/

COPY image-resizer-front/package.json /app/
RUN yarn install

COPY image-resizer-front /app/
RUN yarn build

FROM nginx:alpine

COPY nginx/dev.conf /etc/nginx/nginx.conf
COPY --from=build-deps /app/dist/ /dist/

CMD ["nginx", "-g", "daemon off;"]
