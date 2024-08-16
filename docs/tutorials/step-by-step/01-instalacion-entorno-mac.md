### 1.1: Instalación del Entorno de Desarrollo en una Mac

#### **1.1 Instalación del Entorno de Desarrollo**

Para desarrollar el proyecto **chilaquiler-taskero**, es necesario configurar un entorno de desarrollo adecuado en una Mac. A continuación se describen los pasos para instalar y configurar las herramientas necesarias:

---

#### **1.1.1 Instalación de JDK 21**

1. **Verificar la instalación de Homebrew** (si no está instalado):
   - Homebrew es un gestor de paquetes para macOS que facilita la instalación de software.
   - Abre la terminal y ejecuta:
     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```
   - Una vez instalado, actualiza Homebrew:
     ```bash
     brew update
     ```

2. **Instalar OpenJDK 21**:
   - Ejecuta el siguiente comando en la terminal para instalar OpenJDK 21:
     ```bash
     brew install openjdk@21
     ```
   - Después de la instalación, crea un enlace simbólico para usar Java 21 como la versión predeterminada:
     ```bash
     sudo ln -sfn $(brew --prefix openjdk@21)/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-21.jdk
     ```

3. **Verificar la instalación**:
   - Verifica que Java 21 esté correctamente instalado ejecutando:
     ```bash
     java -version
     ```
   - Deberías ver una salida similar a:
     ```
     openjdk version "21" 2024-03-14
     OpenJDK Runtime Environment (build 21+33)
     OpenJDK 64-Bit Server VM (build 21+33, mixed mode, sharing)
     ```

#### **1.1.2 Instalación de IntelliJ IDEA o VS Code**

1. **IntelliJ IDEA**:
   - Descarga e instala IntelliJ IDEA desde [aquí](https://www.jetbrains.com/idea/download/).
   - Sigue las instrucciones para completar la instalación.

2. **VS Code** (opcional):
   - Descarga e instala Visual Studio Code desde [aquí](https://code.visualstudio.com/).
   - Instala las extensiones recomendadas para Java y Spring Boot:
     - **Java Extension Pack**
     - **Spring Boot Extension Pack**

#### **1.1.3 Instalación de Node.js y Angular CLI**

1. **Instalar Node.js utilizando Node Version Manager (NVM)**:
   - Instala NVM si aún no lo tienes:
     ```bash
     brew install nvm
     mkdir ~/.nvm
     ```
   - Añade las siguientes líneas a tu archivo `.zshrc` (o `.bashrc` si usas bash):
     ```bash
     export NVM_DIR="$HOME/.nvm"
     [ -s "/usr/local/opt/nvm/nvm.sh" ] && \. "/usr/local/opt/nvm/nvm.sh"
     [ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/usr/local/opt/nvm/etc/bash_completion.d/nvm"
     ```
   - Recarga tu terminal:
     ```bash
     source ~/.zshrc
     ```
   - Instala la última versión estable de Node.js:
     ```bash
     nvm install --lts
     nvm use --lts
     ```

2. **Instalar Angular CLI**:
   - Ejecuta el siguiente comando para instalar Angular CLI globalmente:
     ```bash
     npm install -g @angular/cli
     ```
   - Verifica la instalación de Angular CLI:
     ```bash
     ng version
     ```
