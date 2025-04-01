1. Requisitos de Sistema
1.1. Hardware Mínimo
CPU: 2 núcleos (4 recomendados para Jenkins)

RAM: 4 GB (8 GB recomendados para entornos productivos)

Disco: 50 GB de espacio libre (SSD recomendado)

Sistema Operativo: Linux (Ubuntu 20.04/22.04 LTS recomendado) o macOS/Windows (con WSL2)

2. Instalación de Dependencias
2.1. Java (Requisito para Jenkins)
Jenkins requiere Java 11 o Java 17 (recomendado).
Instalación en Ubuntu/Debian:

bash
Copy
sudo apt update
sudo apt install openjdk-17-jdk
Verificar instalación:

bash
Copy
java -version
# Debe mostrar: openjdk 17.x.x
2.2. Jenkins
Instalación en Linux (Ubuntu/Debian):

bash
Copy
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
Iniciar Jenkins:

bash
Copy
sudo systemctl start jenkins
sudo systemctl enable jenkins  # Para que inicie automáticamente
Verificar estado:

bash
Copy
sudo systemctl status jenkins
Acceso inicial:

Abrir en navegador: http://localhost:8080

Desbloquear Jenkins con la contraseña inicial:

bash
Copy
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
3. Configuración de GitHub
3.1. Crear un Fork del Repositorio
Ir a https://github.com/yosoyfunes/nodejs-helloworld-api

Hacer clic en "Fork" (creará una copia en tu cuenta de GitHub).

3.2. Clonar el Repositorio Localmente
bash
Copy
git clone https://github.com/tu-usuario/nodejs-helloworld-api.git
cd nodejs-helloworld-api
3.3. Configurar Git (Opcional, si no está configurado)
bash
Copy
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
4. Instalación de Node.js (usando nvm)
nvm (Node Version Manager) permite gestionar múltiples versiones de Node.js.
Instalación de nvm:

bash
Copy
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc  # Recargar configuración
Instalar Node.js (LTS recomendado):

bash
Copy
nvm install 18  # Última versión LTS
node -v  # Verificar instalación (debe mostrar v18.x.x)
npm -v   # Verificar npm
5. Instalación y Configuración de Ngrok
Ngrok expone Jenkins a Internet para que GitHub pueda enviar webhooks.
Descargar e instalar Ngrok:

bash
Copy
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
Autenticación en Ngrok (requiere cuenta gratuita):

bash
Copy
ngrok config add-authtoken TU_TOKEN_NGROK
Iniciar Ngrok para exponer Jenkins:

bash
Copy
ngrok http 8080
Obtener la URL pública:

Se mostrará una línea como:

Copy
Forwarding https://abc123.ngrok.io -> http://localhost:8080
Esta URL (https://abc123.ngrok.io) se usará en el webhook de GitHub.

6. Plugins Requeridos en Jenkins
Instalar los siguientes plugins desde Manage Jenkins → Manage Plugins → Available plugins:

NodeJS (nodejs-plugin)
