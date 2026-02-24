# -------- Build Stage --------
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install -g @angular/cli
RUN npm install

COPY . .

RUN ng build --configuration production

# -------- Production Stage --------
FROM nginx:alpine

COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]