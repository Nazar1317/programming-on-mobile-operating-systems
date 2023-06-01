Для создания простого приложения на Vuejs я использовал следующие шаги:

   Обязательно устанавливаю Node.js
    Придаю зависимость  npm install
      Новая дериктория 
    Инициализировал новый проект vue create
    Создаю и добавляю код: vue.config.js

module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true
      }
    }
  }
}

6.Запускаю командой npm run serve 7 с установкой конфигурации 

server {
    listen 8000;
    
    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

8.Cтартую командой nginx
