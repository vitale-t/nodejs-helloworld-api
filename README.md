## 1. Instalación de Dependencias

### 1.1. Java (Requisito para Jenkins)

Jenkins requiere **Java 17** (recomendado).

#### Instalación en Ubuntu/Debian:

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

#### Verificar instalación:

```bash
java -version
```

Debe mostrar: `openjdk 17.x.x`

### 1.2. Jenkins

#### Instalación en Linux (Ubuntu/Debian):

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
```

#### Iniciar Jenkins:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins  # Para que inicie automáticamente
```

#### Verificar estado:

```bash
sudo systemctl status jenkins
```

#### Acceso inicial:

Abrir en el navegador: [http://localhost:8080](http://localhost:8080)

Desbloquear Jenkins con la contraseña inicial:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## 2. Configuración de GitHub

### 2.1. Crear un Fork del Repositorio

1. Ir a [https://github.com/yosoyfunes/nodejs-helloworld-api](https://github.com/yosoyfunes/nodejs-helloworld-api)
2. Hacer clic en "Fork" (creará una copia en tu cuenta de GitHub).

### 2.2. Clonar el Repositorio Localmente

```bash
git clone https://github.com/tu-usuario/nodejs-helloworld-api.git
cd nodejs-helloworld-api
```

### 2.3. Configurar Git (Opcional, si no está configurado)

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

## 3. Instalación de Node.js y dependencias

nvm permite gestionar múltiples versiones de Node.js.

### Instalación de nvm:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc  # Recargar configuración
```

### Instalación de Node.js (LTS recomendado):

```bash
nvm install 18  # Última versión LTS
node -v  # Verificar instalación (debe mostrar v18.x.x)
npm -v   # Verificar npm
```

### Instalación de dependencias de la aplicación:

```bash
npm install  # Instalar dependencias
npm test  # Ejecutar pruebas
npm start  # Iniciar el servidor
```

### Realizar una solicitud de prueba:

```bash
curl http://localhost:3000
```

## 4. Instalación y Configuración de Ngrok

Ngrok expone Jenkins a Internet para que GitHub pueda enviar webhooks.

### Descargar e instalar Ngrok:

```bash
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
```

### Iniciar Ngrok para exponer Jenkins:

```bash
ngrok http 8080
```

#### Obtener la URL pública:

Se mostrará una línea como:

```
Forwarding https://abc123.ngrok.io -> http://localhost:8080
```

Esta URL (`https://abc123.ngrok.io`) se usará en el webhook de GitHub.

## 5. Plugins Requeridos en Jenkins

Instalar los siguientes plugins desde **Manage Jenkins** → **Manage Plugins** → **Available plugins**:

- **NodeJS (nodejs-plugin)**


