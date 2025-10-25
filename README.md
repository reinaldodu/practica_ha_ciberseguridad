# 🐳 Práctica Docker: Gestión de Redundancia, Alta Disponibilidad y Ciberseguridad

Esta práctica tiene como propósito aplicar los conceptos de **gestión de redundancia**, **alta disponibilidad** y **ciberseguridad** utilizando **contenedores Docker** dentro del entorno en la nube **GitHub Codespaces**.

El ejercicio se basa en el uso de **HAProxy** como balanceador de carga, junto a dos servidores web simples (**Web1** y **Web2**) que demuestran cómo distribuir peticiones de manera equitativa para garantizar **disponibilidad continua** ante posibles fallas o sobrecarga en un servidor.

---

## 🧱 Objetivos de aprendizaje

Al finalizar esta práctica, el estudiante será capaz de:

- Comprender los conceptos de **redundancia** y **alta disponibilidad**.  
- Implementar un **balanceador de carga** con **HAProxy**.  
- Ejecutar servicios web simultáneos dentro de **contenedores Docker**.  
- Analizar el comportamiento del tráfico balanceado entre servidores.  
- Identificar técnicas básicas de **ciberseguridad** aplicadas al despliegue de contenedores.

---

## ☁️ Entorno de trabajo

Para realizar esta práctica no necesitas instalar nada en tu computador.
Todo se desarrollará directamente en la nube usando **GitHub Codespaces**.

🔹 Pasos iniciales:

1. Ingresa a 👉 <a href="https://github.com/codespaces" target="_blank">GitHub Codespaces</a>
2. Selecciona la plantilla Blank (entorno vacío).
3. Espera a que se abra el entorno de desarrollo basado en VS Code Web.
4. Una vez cargado, podrás ejecutar todos los comandos desde la **terminal** integrada.

---

### 1️⃣ Clonar el repositorio

Ejecuta en la terminal:

```bash
git clone https://github.com/reinaldodu/practica_ha_ciberseguridad.git
   ```
Luego entra al directorio del proyecto:
```bash
cd practica_ha_ciberseguridad
   ```
### 2️⃣ Ejecutar los contenedores

Inicia los servicios definidos en el archivo docker-compose.yml:
```bash
docker compose up -d
   ```
Este comando crea y ejecuta los contenedores:
- **web1**: primer servidor web
- **web2**: segundo servidor web
- **haproxy**: balanceador de carga

### 3️⃣ Verificar el estado de los contenedores
Comprueba que todos estén en ejecución:
```bash
docker compose ps
   ```
   
### 4️⃣ Acceder al balanceador de carga
Abre el puerto 8080 en Codespaces y accede al sitio web.
Haz clic en la pestaña puertos (en la barra inferior) y luego en el icono de navegación.
![Puertos](https://i.postimg.cc/GpRjJPSV/puertos.png)

Verás una página similar a esta:
![Respuesta](https://i.postimg.cc/pdvBYQ1g/respuesta.png)
Actualiza la página varias veces para ver cómo HAProxy distribuye las peticiones entre web1 y web2.

### 5️⃣ Simular una caída del servidor web1
Detén el contenedor web1:
```bash
docker compose stop web1
   ```
Actualiza la página del puerto 8080 varias veces.
👉 Notarás que ahora solo responde el servidor web2

### 6️⃣ Simular caída de web2

Detén ahora web2:
```bash
docker compose stop web2
   ```
Actualiza la página del puerto 8080:
👉 Verás que HAProxy no puede dirigir las solicitudes, ya que ambos servidores web están fuera de servicio.

### 7️⃣ Restaurar los servicios web
Vuelve a iniciar ambos servidores:
```bash
docker compose start web1 web2
   ```
Actualiza nuevamente el navegador:
✅ El balanceador vuelve a distribuir el tráfico entre web1 y web2.

### 8️⃣ Monitorear y auditar la infraestructura

Para revisar el comportamiento de los contenedores, ejecuta:
```bash
docker logs web1
   ```
```bash
docker logs web2
   ```
```bash
docker stats
   ```

También puedes usar el plugin **Docker** para VS Code, con el fin de monitorear los Contenedores Docker.
