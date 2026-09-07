# Tarea 1 - Configuración del entorno de desarrollo Python y Docker usando WSL con Ubuntu

Documentación paso a paso para crear un entorno de desarrollo baso en Linux (Ubuntu) usando una computadora con Windows.

## 1. Instalación de WSL con Ubuntu
Para habilitar la distribución Linux  por defecto(Ubuntu) en Windows, se debe ejecutar la instalación mediante la consola de comandos de Windows(PowerShell).
### Pasos a ejecutar:
1. Abrir PowerShell como administrador:
* Presionar la tecla de `Windows`
* Buscar **PowerShell**
* **Ejecutarlo como administrador**
2. Ejecutar comando para instalar WSL:
```bash 
wsl --install 
```
3. Comprobación
* Ejecutar dentro de la terminal Ubuntu:
```bash
lsb_release -a
```
Deberá parecer lo siguiente `Description: Ubuntu XX.XX LTS`

4. Volver a abrir instancia de Ubuntu:
* Abrir PowerShell e ejecutar:
```bash 
wsl -d Ubuntu
```
**Si es la primera vez que se utilizan características de virtualización, se deberá reiniciar la computadora. Al volver a iniciar, se abrirá una consola de Ubuntu para finalizar el proceso**

## 2. Comandos iniciales
Una vez dentro de la consola Ubuntu se pueden ejecutar los siguientes comandos básicos.

1. Ir a la carpeta Home:
```bash
cd ~
```
2. Mostrar ruta absoluta:
```bash
pwd
```
3. Listar archivos y carpetas:
```bash
ls
```
4. Crear carpeta:
```bash
mkdir nombre_carpeta
```
5. Moverse entre carpetas:
```bash
cd nombre_carpeta
```
6. Volver a carpeta anterior:
```bash
cd ..
```
7. Crear archivo vacío:
```bash
touch archivo.txt
```

8. Mostrar contenido de un archivo:
```bash
cat archivo.txt
```
9. Antes de instalar cualquier cosa:
```bash
sudo apt update
sudo apt upgrade
``` 
## 3. Instalación y Configuración de Docker
Antes de empezar a instalar Docker se tiene que eliminar algunos paquetes que podrían generar algún conflicto.

1. Desinstalar versiones antiguas o paquetes conflictivos:
``` bash
sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc docker-buildx podman-docker containerd runc | cut -f1)
```
2. Configurar el repositorio oficial de Docker
Para instalar la versión mas reciente de Docker y recibir actualizaciones:
```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
3. Instalar Docker engine:
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

4. Verificar instalación:
```bash
sudo docker run hello-world
```
Si la instalación se hizo de manera exitosa mostrara un mensaje comenzando por `Hello from Docker!`

**Pasos importantes después de instalar Docker**
Pasos para ejecutar Docker sin permisos de super usuario (sudo).

5. Crear el grupo de Docker:
```bash
sudo groupadd docker
```

6. Agregar el usuario actual ($USER) al grupo Docker:
```bash
sudo usermod -aG docker $USER
```
7. Aplicar los cambios de grupo:
```bash
newgrp docker
```
Si el comando anterior no funciona se tiene que reiniciar la terminal.

8. Verificar que el comando se ejecute sin uso de sudo:
```bash
docker run hello-world
```
## 4. Configuración del Entorno de Python y Virtualenv
Gestionar diferentes versiones de Python sin alterar la versión del sistema operativo.
1. Instalar los paquetes necesarios para compilar el código fuente:
 ```bash 
 sudo apt install -y \ make \ build-essential \ libssl-dev \ zlib1g-dev \ libbz2-dev \ libreadline-dev \ libsqlite3-dev \ curl \ llvm \ libncursesw5-dev \ xz-utils \ tk-dev \ libxml2-dev \ libxmlsec1-dev \ libffi-dev \ liblzma-dev
 ```
 2. Instalar y configurar Pyenv:
  ```bash
  git clone [https://github.com/pyenv/pyenv.git](https://github.com/pyenv/pyenv.git) ~/.pyenv
   ```
   Para verificar que se clono correctamente:
   ```bash
   ls ~/.pyenv
   ```
   3. Configuración de las variables de entorno:
  ```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc
```
4. Instalar la versión seleccionada de pyenv (3.14.7)
```bash
pyenv install 3.14.7
```
5. Verificar que se instalara y activarla de forma global:
```bash
pyenv versions
pyenv global 3.14.7
pyenv rehash
```
## 5. Despliegue e Inicio de Jupyter Notebook vía CLI
1. Crear y acceder al directorio
```bash
mkdir -p ~/jupyter
cd ~/jupyter
```
2. Crear el entorno virtual:
```bash
python -m venv .venv
```
3. Activar el entorno virtual:
```bash
source .venv/bin/activate
```
Cuando se active en entorno virtual aparecerá `.venv` al inicio de la línea de comandos.

4. Actualizar el gestor de paquetes pip:
```bash
python -m pip install --upgrade pip
```
5. Instalar paquetes necesarios **en el entorno virtual**:
```bash
pip install notebook ipykernel
```
6. Ejecutar la interfaz web de Jupyter Notebook:
```bash
jupyter notebook
```
La consola mostrara un URL, puedes hacer clic derecho en el enlace para abrir la interfaz de Jupyter Notebook.
