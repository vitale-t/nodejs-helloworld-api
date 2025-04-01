## 1. Configuración de GitHub

### 1.1. Crear un Fork del Repositorio

1. Ir a [https://github.com/yosoyfunes/nodejs-helloworld-api](https://github.com/yosoyfunes/nodejs-helloworld-api)
2. Hacer clic en "Fork" (creará una copia en tu cuenta de GitHub).

### 1.2. Clonar el Repositorio Localmente

```bash
git clone https://github.com/tu-usuario/nodejs-helloworld-api.git
cd nodejs-helloworld-api
```

### 1.3. Configurar Git (Opcional, si no está configurado)

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

## 2. Instalación de Node.js y dependencias

nvm permite gestionar múltiples versiones de Node.js.

### 2.2. Instalación de nvm:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc  # Recargar configuración
```

### 2.3. Instalación de Node.js (LTS recomendado):

```bash
nvm install 18  # Última versión LTS
node -v  # Verificar instalación (debe mostrar v18.x.x)
npm -v   # Verificar npm
```

### 2.4. Instalación de dependencias de la aplicación:

```bash
npm install  # Instalar dependencias
npm test  # Ejecutar pruebas
npm start  # Iniciar el servidor
```

### Realizar una solicitud de prueba:

```bash
curl http://localhost:3000
```

## 3. Instalación y Configuración de Ngrok

Ngrok expone Jenkins a Internet para que GitHub pueda enviar webhooks.

### 3.1. Descargar e instalar Ngrok:

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
```

### 3.2 Iniciar Ngrok para exponer Jenkins:

```bash
ngrok http 8080
```

### 3.3 Obtener la URL pública:

Se mostrará una línea como:

```
Forwarding https://abc123.ngrok.io -> http://localhost:8080
```

Esta URL (`https://abc123.ngrok.io`) se usará en el webhook de GitHub.

## 4. Plugins Requeridos en Jenkins

Instalar los siguientes plugins desde **Manage Jenkins** → **Manage Plugins** → **Available plugins**:

- **NodeJS (nodejs-plugin)**
