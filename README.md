# PM3 - Grupo 6

## Infraestrutura

| VM | Função | IP |
|---|---|---|
| VM1 | Frontend (Nginx + Angular) | 192.168.1.16 |
| VM2 | Backend (Spring Boot) | 192.168.1.17 |
| VM3 | Banco (MariaDB + Keycloak) | 192.168.1.15 |

## Pré-requisitos

- Docker e Docker Compose instalados em cada VM
- Alpine Linux
- Certificados SSL (solicitar ao grupo)

## Domínios - adicionar no /etc/hosts

192.168.1.16    sistema1.net sistema2.net
192.168.1.15    auth.projeto.local

## Como subir o Frontend (VM1)

1. Instalar Docker na VM:
apk add docker docker-openrc docker-cli-compose
rc-update add docker boot
service docker start

2. Copiar certificados para a VM:
scp fullchain.pem wildcard.key frontend@192.168.1.16:/tmp/

3. Na VM do frontend:
mkdir -p /opt/frontend/ssl
mv /tmp/fullchain.pem /opt/frontend/ssl/
mv /tmp/wildcard.key /opt/frontend/ssl/
cd /opt/frontend
docker compose up -d

## Keycloak

- URL: http://192.168.1.15:8080
- Realm: zadinventory
- Admin: admin / admin
- Roles: sys1_admin, sys1_user, sys1_exclusivo1, sys1_exclusivo2

## Tecnologias

- Frontend: Angular 19
- Backend: Spring Boot (Java 17)
- Banco: MariaDB 11.4
- Auth: Keycloak 24.0
- Web Server: Nginx Alpine
- Containers: Docker + Docker Compose