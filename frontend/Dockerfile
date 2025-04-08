FROM node:18-alpine

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build --prod

RUN npm install -g http-server

EXPOSE 3000

CMD ["http-server", "dist/angular-15-crud", "-p", "3000", "-c-1"]



