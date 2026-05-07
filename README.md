##Мой проект мониторинга сервера
В качестве основы взят VPS c ОС ubuntu 24.04.
Мониторинг производится с помощью Prometheus, Node exporter; Графики строятся с помощью Grafana;
Алерты отправляются в телеграм бота через Alertmanager. В качестве reverse-proxy используется Nginx.
Реализована возможность зайти в веб интерфейс Grafana и Prometheus из интернета.

Данный стек мониторит основные жизненные показатели сервера такие как средняя нагрузка на ЦП, загрузка ОЗУ,
свободное место на диске /, также доступность контейнеров.

##Инструкция по применению

#Клонируем репозиторий
git clone https://github.com/t44rbo/monitoring-stack.git
cd monitoring-stack

#Создаем файл с секретами
nano .env 

#Заполняем переменные в файле .env

GF_ADMIN_PASSWORD=ваш пароль
GF_ADMIN_USER=admin
TG_BOT_TOKEN=токен вашего тг бота
TG_CHAT_ID=ваш чат ИД

# Создаём файл с логином и хешем пароля
# Замени "твой_пароль" на свой
echo "admin:$(openssl passwd -apr1 'твой_пароль')" > nginx/.htpasswd

##Структура папок
monitoring-stack/
├── .env
├── .gitignore
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml
│   └── alert.rules.yml
├── alertmanager/
│   └── alertmanager.yml
└── nginx/
    └── nginx.conf
    |_ .htpaswd    
