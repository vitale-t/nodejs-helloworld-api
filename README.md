# NodeJS App en Jenkinsfile

## 1. Configuración de GitHub

### 1.1. Crear un Fork del Repositorio

1. Ir a [https://github.com/yosoyfunes/nodejs-helloworld-api](https://github.com/yosoyfunes/nodejs-helloworld-api)
2. Hacer clic en "Fork" (creará una copia en tu cuenta de GitHub).

### 1.2. Clonar el Repositorio Localmente

```bash
git clone https://github.com/tu-usuario/nodejs-helloworld-api.git
cd nodejs-helloworld-api
```

### 1.3. Configurar Git

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

## 2. Instalación de Node.js y NVM

Node.js es un entorno de ejecución de JavaScript de código abierto y multiplataforma. Para gestionar múltiples versiones de Node.js, utilizamos NVM (Node Version Manager).

### 2.1 Descargar e instalar NVM:
Para instalar o actualizar NVM, ejecuta uno de los siguientes comandos:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

O utilizando `wget`:

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

Estos comandos descargan un script que clona el repositorio de NVM en `~/.nvm` y agrega las líneas de configuración necesarias en el archivo de perfil correspondiente (`~/.bashrc`, `~/.bash_profile`, `~/.zshrc`, o `~/.profile`).

Si la instalación afecta el archivo de perfil incorrecto, establece la variable de entorno `$PROFILE` con la ruta del archivo de perfil adecuado antes de ejecutar el script nuevamente.

### 2.2 Activar NVM sin reiniciar la terminal:
```sh
\. "$HOME/.nvm/nvm.sh"
```

### 2.3 Descargar e instalar Node.js:
```sh
nvm install 18
```

### 2.4 Verificar la versión de Node.js y npm:
```sh
node -v # Debería mostrar "v18.20.8"
nvm current # Debería mostrar "v18.20.8"
npm -v # Debería mostrar "10.8.2"
```

---

## 3. Instalación del plugin de NodeJS en Jenkins

Este plugin proporciona integración de Jenkins con NodeJS y npm.

### 3.1 Instalación a través de la interfaz gráfica:
1. Desde el panel de Jenkins, ve a **Administrar Jenkins > Administrar plugins**.
2. Selecciona la pestaña **Disponibles**.
3. Busca "nodejs" y selecciona el plugin para instalarlo.

### 3.2 Instalación usando la CLI:
```sh
jenkins-plugin-cli --plugins nodejs:1.6.4
```

### 3.3 Instalación manual:
Descarga la versión requerida del plugin y cárgala manualmente en el controlador de Jenkins.

## 5. Instalación y Configuración de Ngrok

Ngrok expone Jenkins a Internet para que GitHub pueda enviar webhooks.

### 5.1. Descargar e instalar Ngrok:

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
```

### 5.2 Iniciar Ngrok para exponer Jenkins:

```bash
ngrok http 8080
```

### 5.3 Obtener la URL pública:

Se mostrará una línea como:

```
Forwarding https://abc123.ngrok.io -> http://localhost:8080
```

Esta URL (`https://abc123.ngrok.io`) se usará en el webhook de GitHub.

## 6. Plugins Requeridos en Jenkins

Instalar los siguientes plugins desde **Manage Jenkins** → **Manage Plugins** → **Available plugins**:

- **NodeJS (nodejs-plugin)**
