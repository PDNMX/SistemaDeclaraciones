# Taller de Capacitadores del Sistema Declaraciones
Recursos del Taller de instalación y despliegue del sistema de declaraciones en una sistema operativo Ubuntu Server 20 LTS.

# Comandos y configuraciones presentadas en el taller
<details>
  <summary>Instalación de docker y docker-compose</summary>
  
  ```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce docker-compose
sudo systemctl status docker
sudo systemctl enable docker
sudo usermod -aG docker ${USER}
su - ${USER}
id -nG
  ```
</details>


<details>
  <summary>Instalación de NGINX</summary>
  
  ```bash
sudo apt install nginx
sudo systemctl status nginx
sudo systemctl enable nginx
  ```
</details>

<details>
  <summary>Instalación MongoDB</summary>
  
  ```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
sudo apt update
sudo apt install mongodb-org
sudo systemctl start mongod.service
sudo systemctl enable mongod.service
sudo systemctl status mongod.service

mongo --host localhost
use admin
db.createUser({user: "declara-user", pwd: "declara-password", roles: [{ role: "dbOwner", db: "declaraciones" } ] })
```
</details>

<details>
  <summary>Configuración NGINX</summary>
  
```nginx
server {
        listen 80;
        server_name dominio-o-ip;
        location / {
            proxy_pass http://localhost:8080;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }

        location /api {
     	    rewrite /api(/.*)$ $1 break;
            proxy_pass http://localhost:3000;
            proxy_http_version 1.1;
            proxy_set_header   X-Forwarded-For $remote_addr;
            proxy_set_header   Host $http_host;
        }
}
```
</details>

<details>
  <summary>Cambiar un usuario a rol de ROOT</summary>

  ```bash
mongo -u declara-user -p --authenticationDatabase "admin" declaraciones
db.users.find().pretty();
var usuario = db.users.findOne({"_id": ObjectId("AQUI-VA-EL-ID")});
usuario.roles = [ "ROOT" ];
db.users.save(usuario);
 ```
</details>


