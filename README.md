# Docker Termix SSH 🖥️

Termix es una plataforma web de gestión de servidores profesional, open source y completamente self-hosted que proporciona acceso SSH, gestión de archivos, túneles y herramientas de infraestructura desde un único dashboard web. Es la alternativa gratuita y autohospedable ideal para quienes gestionan múltiples servidores sin querer depender de servicios de pago como Termius.

## 🚀 Características Principales

- **Terminal SSH Web:** Acceso total a tus servidores desde cualquier navegador, sin necesidad de clientes locales.
- **Split Screen:** Divide tu terminal en hasta 4 paneles simultáneamente para trabajo paralelo.
- **Gestor de Archivos Remoto:** Sube, descarga y edita archivos directamente desde la interfaz web con soporte para sudo.
- **Túneles SSH:** Creación y gestión de túneles con auto-reconexión y monitoreo de estado.
- **Gestión de Docker:** Controla tus contenedores (start/stop/pause/remove) directamente desde la UI.
- **Jump Hosts:** Soporte automatizado para conexiones a través de hosts intermedios.
- **Seguridad Avanzada:** Autenticación TOTP (2FA), verificación de host keys y soporte para SSH Keys.
- **PWA & Mobile:** Acceso remoto optimizado desde dispositivos iOS y Android.

## 🛠️ Requisitos del Sistema

- **RAM:** 1-2 GB (Backend Node.js).
- **Almacenamiento:** 2 GB o más para base de datos y logs.
- **Puerto:** 8080 (Web Dashboard).
- **Software:** Docker y Docker Compose instalados.

## 📦 Instalación con Docker Compose

### 1. Preparar el entorno
Crea la carpeta del proyecto y entra en ella:
```bash
mkdir termix-ssh && cd termix-ssh
```

### 2. Crear el archivo `docker-compose.yml`
Copia el contenido del archivo `docker-compose.yml` incluido en este repositorio.

### 3. Desplegar el servicio
```bash
docker compose up -d
```

### 4. Acceder al Dashboard
Abre tu navegador y entra en: `http://localhost:8080`

## ⚙️ Primeros Pasos

1. **Configuración Inicial:** Al entrar por primera vez, crea tu cuenta de administrador.
2. **Agregar Servidores:** Ve a **Dashboard $\rightarrow$ Add New Host**. Ingresa el hostname/IP, usuario y el método de autenticación (Password o SSH Key).
3. **Conexión:** Haz clic en el servidor desde el dashboard para abrir la terminal web.
4. **Túneles:** Crea túneles SSH desde el dashboard definiendo los puertos locales y remotos.

## 🛡️ Seguridad y Mantenimiento

- **HTTPS:** Termix transmite credenciales sensibles. Se recomienda encarecidamente usar un proxy inverso como **Caddy** o **Nginx** para habilitar HTTPS.
- **SSH Keys:** Prioriza el uso de llaves SSH sobre contraseñas para gestionar tus servidores.
- **Logs:** `docker logs -f termix`
- **Backup de Datos:** 
  ```bash
  docker run --rm -v termix-data:/data -v $(pwd):/backup alpine tar czf /backup/termix-backup-$(date +%Y%m%d).tar.gz -C /data .
  ```
- **Actualización:** `docker compose pull && docker compose up -d`

---
*Basado en el tutorial de [Genbyte](https://genbyte.blogspot.com/)*
