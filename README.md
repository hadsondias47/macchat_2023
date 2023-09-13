
**NOTE**: A nova versão do whatsapp-web.js requer o Node 14. Atualize suas instalações para continuar usando.

Um sistema de tickets _muito simples_ baseado em mensagens do WhatsApp.

Backend uses [whatsapp-web.js]
para receber e enviar mensagens do WhatsApp, criar tickets a partir delas e armazenar tudo em um MySQL database.

Frontend É um _chat app_ multiusuário completo inicializado com react-create-app e Material UI, que se comunica com o back-end usando REST API e Websockets. Permite interagir com contatos, tickets, enviar e receber mensagens do WhatsApp.

**NOTE**: Não posso garantir que você não será bloqueado usando esse método, embora tenha funcionado para mim. O WhatsApp não permite bots ou clientes não oficiais em sua plataforma, então isso não deve ser considerado totalmente seguro.


## Instalação e Uso (Linux Ubuntu )


Criar banco de dados Mysql usando docker:

_Note_: change MYSQL_DATABASE, MYSQL_PASSWORD, MYSQL_USER and MYSQL_ROOT_PASSWORD.

```bash
docker run --name db -e MYSQL_ROOT_PASSWORD=strongpassword -e MYSQL_DATABASE= -e MYSQL_USER= -e MYSQL_PASSWORD= --restart always -p 3306:3306 -d mariadb:latest --character-set-server=utf8mb4 --collation-server=utf8mb4_bin

# Ou execute usando `docker-compose` como abaixo
# Antes de copiar .env.example para .env primeiro e definir as variáveis ​​no arquivo.
docker-compose up -d mysql

# Para administrar este banco de dados mysql facilmente usando phpmyadmin. 
# Ele será executado por padrão na porta 9000, mas pode ser alterado em .env usando `PMA_PORT`
docker-compose -f docker-compose.phpmyadmin.yaml up -d
```

Instalação dependencia puppeteer:

```bash
sudo apt-get install -y libxshmfence-dev libgbm-dev wget unzip fontconfig locales gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils
```

```bash
cp .env.example .env
nano .env
```



```bash
NODE_ENV=DEVELOPMENT      
BACKEND_URL=http://localhost
FRONTEND_URL=https://localhost:3000
PROXY_PORT=8080
PORT=8080

DB_HOST=                  
DB_DIALECT=
DB_USER=
DB_PASS=
DB_NAME=

JWT_SECRET=3123123213123
JWT_REFRESH_SECRET=75756756756
```

Instalação backend dependencias:

```bash
npm install
npm run build
npx sequelize db:migrate
npx sequelize db:seed:all
```

iniciar backend:

```bash
npm start
```

