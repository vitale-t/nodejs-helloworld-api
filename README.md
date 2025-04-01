# NodeJS App en Jenkinsfile

Este repositorio contiene una API simple de Node.js como demostración para la integración continua con Jenkins y GitHub Webhooks.

## 1. Configuración de GitHub

### 1.1. Crear un Fork del Repositorio
1. Ir a https://github.com/yosoyfunes/nodejs-helloworld-api.
2. Hacer clic en "Fork" (creará una copia en tu cuenta de GitHub).

### 1.2. Clonar el Repositorio Localmente
```sh
git clone https://github.com/tu-usuario/nodejs-helloworld-api.git
cd nodejs-helloworld-api
```

## 2. Instalación de Node.js y NVM

Node.js es un entorno de ejecución de JavaScript de código abierto y multiplataforma. Para gestionar múltiples versiones de Node.js, utilizamos Node Version Manager.

### 2.1 Descargar e instalar Node Version Manager
Para instalar o actualizar Node Version Manager, ejecuta uno de los siguientes comandos:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```
O utilizando wget:
```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

Si la instalación afecta el archivo de perfil incorrecto, establece la variable de entorno `$PROFILE` con la ruta del archivo de perfil adecuado antes de ejecutar el script nuevamente.

### 2.2 Activar Node Version Manager sin reiniciar la terminal
```sh
\. "$HOME/.nvm/nvm.sh"
```

### 2.3 Descargar e instalar Node.js
```sh
nvm install 18
```

### 2.4 Verificar la versión de Node.js y Node Package Manager
```sh
node -v # Debería mostrar "v18.20.8"
nvm current # Debería mostrar "v18.20.8"
npm -v # Debería mostrar "10.8.2"
```
Para más información, consulta:
- https://nodejs.org/es/download
- https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating

## 3. Instalación del plugin de Node.js en Jenkins

Este plugin proporciona integración de Jenkins con Node.js y Node Package Manager.

### 3.1 Instalación a través de la interfaz gráfica
1. Desde el panel de Jenkins, ve a Administrar Jenkins > Administrar plugins.
2. Selecciona la pestaña Disponibles.
3. Busca "nodejs" y selecciona el plugin para instalarlo.

### 3.2 Instalación usando la línea de comandos
```sh
jenkins-plugin-cli --plugins nodejs:1.6.4
```

### 3.3 Instalación manual
Descarga la versión requerida del plugin y cárgala manualmente en el controlador de Jenkins.

### 3.4 Configuración
Para más detalles sobre la configuración avanzada, visita la documentación oficial del plugin de Node.js en Jenkins: https://plugins.jenkins.io/nodejs/.

## 4. Instalación y Configuración de Ngrok

Ngrok expone Jenkins a Internet para que GitHub pueda enviar webhooks.

### 4.1 Descargar e instalar Ngrok
```sh
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
```

### 4.2 Iniciar Ngrok para exponer Jenkins
```sh
ngrok http 8080
```

### 4.3 Obtener la URL pública
Se mostrará una línea como:
```sh
Forwarding https://abc123.ngrok.io -> http://localhost:8080
```

## 5. Configurar GitHub Webhook
Para iniciar automáticamente un job en Jenkins cada vez que se realice un push o se cree un pull request:
1. Ir al repositorio en GitHub.
2. Navegar a Configuración > Webhooks.
3. Hacer clic en "Agregar webhook".
4. En el campo "Payload URL", ingresar la URL pública del servicio de Jenkins (expuesta con Ngrok).
5. Seleccionar el contenido "application/json".
6. Configurar los eventos de disparo ("Solo el evento push" o "Déjame seleccionar eventos individuales").
7. Guardar los cambios.

Para más detalles, consultar la documentación oficial en https://docs.github.com/es/webhooks/about-webhooks.

## 6. Documentación de Referencia
| Título | Descripción | URL |
|--------|-------------|-----|
| Ngrok Developer Ingress | Permite exponer un servicio local hacia internet | https://ngrok.com/ |
| GitHub Webhooks | Documentación oficial sobre los webhooks | https://docs.github.com/es/webhooks/about-webhooks |
| Jenkins GitHub Plugin | Plugin utilizado para integrar Webhooks de GitHub a Jenkins | https://plugins.jenkins.io/github/ |
| Instalar Node Version Manager para Node.js | Guía para instalar Node Version Manager en Linux | https://nodejs.org/en/download/package-manager |

---
