#STAGE 1
FROM node:20.18.0 AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build


#STAGE 2
FROM nginx:alpine
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist/ultra-bank-frontend/browser /usr/share/nginx/html
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]

# Stage 1: Build the Angular application
FROM node:20.18.0 as build

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем package.json и package-lock.json и устанавливаем зависимости
COPY package*.json ./
RUN npm install

# Копируем весь код Angular в контейнер
COPY . .

# Компилируем Angular-приложение
RUN npm run build --prod

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Копируем сгенерированные файлы из предыдущего этапа
COPY --from=build /app/dist/ultra-bank-frontend /usr/share/nginx/html

# Копируем конфигурационный файл Nginx (опционально)
COPY nginx.conf /etc/nginx/nginx.conf

# Expose порта, на котором работает Nginx
EXPOSE 80

# Запускаем Nginx
CMD ["nginx", "-g", "daemon off;"]