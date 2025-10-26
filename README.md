# Termix en Docker | Servidor SSH con gestión web

**Termix** es un servidor SSH moderno con panel web para gestión remota, ejecución de comandos y control de sesiones. Ideal para entornos DevOps o administración remota sin exponer directamente SSH al exterior.

📦 **Servicios incluidos**
- Termix (API + panel web)
- Volumen persistente para configuración y claves

---

⚙️ **docker-compose.yml**
```yaml
services:
  termix:
    image: termixssh/termix:latest
    container_name: termix
    restart: unless-stopped
    ports:
      - "2222:22"      # Puerto SSH
      - "8082:8080"    # Interfaz web
    environment:
      - TZ=Europe/Madrid
      - TERMIX_ADMIN_USER=admin
      - TERMIX_ADMIN_PASS=admin123
    volumes:
      - ./config:/etc/termix
      - ./data:/var/lib/termix
```

---

▶️ **Instrucciones de uso**

1. **Crear el archivo `docker-compose.yml`**  
   Colócalo en una carpeta, por ejemplo `/docker/termix`.

2. **Arrancar Termix**
   ```bash
   docker compose up -d
   ```

3. **Acceder al panel web**
   👉 `http://localhost:8082`  
   Usuario: `admin`  
   Contraseña: `admin123`

4. **Conectarte por SSH**
   ```bash
   ssh admin@localhost -p 2222
   ```
   (Sustituye `localhost` por la IP del servidor si accedes desde la LAN)

---

🧹 **Comandos útiles**
- Ver logs:
  ```bash
  docker logs -f termix
  ```
- Detener el contenedor:
  ```bash
  docker compose down
  ```
- Reiniciar el servicio:
  ```bash
  docker compose restart termix
  ```

---

🧱 **Volúmenes y persistencia**
La configuración y claves SSH se almacenan en `./config` y `./data`, permitiendo mantener usuarios y sesiones entre reinicios.
