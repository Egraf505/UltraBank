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
RUN npm run build

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Копируем сгенерированные файлы из предыдущего этапа
COPY --from=build /app/dist/ultra-bank-frontend/browser /usr/share/nginx/html

# Копируем конфигурационный файл Nginx (опционально)
COPY nginx.conf /etc/nginx/nginx.conf

# Expose порта, на котором работает Nginx
EXPOSE 3000

# Запускаем Nginx
CMD ["nginx", "-g", "daemon off;"]