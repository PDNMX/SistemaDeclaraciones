# Taller del Sistema Declaraciones
Recursos del Taller de instalación y despliegue del sistema de declaraciones:
- [Video](https://youtu.be/lIyRjjGqCd4)
- [Presentación](presentacion.pdf)


# Comandos y configuraciones vistas en el taller
<details>
  <summary>Crear un usuario en mongo</summary>

  ```bash
use admin
db.createUser({user: "declara-user", pwd: "declara-password", roles: [{ role: "dbOwner", db: "declaraciones" }]})
  ```
</details>

<details>
  <summary>Generear o recrear un contenedor con docker-compose</summary>
  
  ```bash
  docker-compose -p declaraciones-backend up -d --build --force-recreate
  ```
</details>

<details>
  <summary>Configuración nginx sin HTTPS</summary>
  
```nginx
server {
	listen 80;
	server_name declaraciones.site;
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
		proxy_set_header X-Forwarded-For $remote_addr;
		proxy_set_header Host $http_host;
	}
}
```
</details>

<details>
  <summary>Recargar configuración de nginx</summary>

  ```bash
  sudo nginx -s reload
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

<details>
  <summary>Generar certificado con acme.sh</summary>

  ```bash
sudo su
cd ~
curl https://get.acme.sh | sh -s email=[sarodriguez@sesna.gob.mx](mailto:sarodriguez@sesna.gob.mx)
source ~/.bashrc
acme.sh --issue -d declaraciones.site --nginx
mkdir -p /etc/nginx/ssl/declaraciones.site
acme.sh --install-cert -d declaraciones.site --key-file /etc/nginx/ssl/declaraciones.site/declaraciones.site.key --fullchain-file /etc/nginx/ssl/declaraciones.site/declaraciones.site.cer
 ```
</details>

<details>
  <summary>Configuración nginx con HTTPS</summary>

  ```nginx
server {
	listen 80;
	server_name declaraciones.site;
	return 301 https://declaraciones.site$request_uri;
}
server {
	listen [::]:443 ssl ipv6only=on;
	listen 443 ssl;
	server_name declaraciones.site;
	ssl_certificate /etc/nginx/ssl/declaraciones.site/declaraciones.site.cer;
	ssl_certificate_key /etc/nginx/ssl/declaraciones.site/declaraciones.site.key;
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
		proxy_set_header X-Forwarded-For $remote_addr;
		proxy_set_header Host $http_host;
	}
}
 ```
</details>


