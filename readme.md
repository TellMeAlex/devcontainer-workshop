# Índice para la Preparación del Taller de DevContainer

1. **Introducción**
  - Objetivos del taller
    ```
    El objetivo de este taller es que los asistentes aprendan que son los DevContainers, como se pueden configurar y personalizar, y como pueden ayudar a mejorar la productividad de los desarrolladores. Además, se mostrarán buenas prácticas y recomendaciones para su uso en proyectos reales.
    ```
  - Requisitos previos
    ```
    Para poder seguir el taller, es necesario tener instalados Docker y Visual Studio Code. 
    ```


2. **Configuración del Entorno**
  - Instalación de Docker
    
    Para instalar Docker, podemos seguir los pasos indicados en la [documentación oficial](https://docs.docker.com/get-docker/).
    En nuestro caso vamos a utilizar WSL2 como base para instalar Docker. Para ello, primero debemos instalar WSL2 siguiendo los pasos indicados en la [documentación oficial](https://docs.microsoft.com/es-es/windows/wsl/install). Una vez instalado WSL2, podemos instalar Docker instalando la versión comunitaria con un [script](https://github.com/docker/docker-install) de instalación: 
    ```
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    ```
    
  - Instalación de Visual Studio Code
    
    Para instalar Visual Studio Code, podemos descargar el instalador desde la [página oficial](https://code.visualstudio.com/Download) y seguir los pasos indicados en la [documentación oficial](https://code.visualstudio.com/docs/setup/setup-overview).
  - Extensiones necesarias
   
    Para poder trabajar con DevContainers, necesitamos instalar la extensión `Remote - Containers` en Visual Studio Code. Para ello, podemos abrir Visual Studio Code, ir a la pestaña de extensiones y buscar la extensión `Remote - Containers` e instalarla. O bien, podemos instalarla desde la línea de comandos con el siguiente comando:
    ```
    code --install-extension ms-vscode-remote.remote-containers
    ```
  - Clonación del repositorio de ejemplo
  
    Para poder seguir el taller, es necesario clonar el repositorio de ejemplo. Para ello, podemos ejecutar el siguiente comando en una terminal:
    ```
    git clone www.github.com/TellMeAlex/devcontainer-workshop
    ```
    La descripción del repositorio es la siguiente:
    ```
    Este repositorio contiene un proyecto de ejemplo para mostrar como configurar y usar DevContainers en Visual Studio Code. El proyecto es una aplicación web sencilla escrita en JavaScript con Node.js y Express. Y un Frontend con React.

    También se incluye un archivo devcontainer.json con la configuración del DevContainer, que se puede usar para crear un entorno de desarrollo aislado y preconfigurado para este proyecto.
    ```

3. **Creación del DevContainer**
  - Estructura del proyecto

    La estructura del proyecto es la siguiente:
    ```
    - backend
      - src
      - package.json
      - Dockerfile
    - frontend
      - src
      - package.json
      - Dockerfile
    - devcontainer.json
    ```
  
  - Archivo `devcontainer.json`

    ```json
    {
        "name": "Node.js & React",
        "build": {
            "dockerfile": "Dockerfile",
            "context": "..",
            "args": {
                "VARIANT": "14-bullseye"
            }
        },
        "settings": {
            "terminal.integrated.shell.linux": "/bin/bash"
        },
        "extensions": [
            "dbaeumer.vscode-eslint",
            "esbenp.prettier-vscode",
            "ms-azuretools.vscode-docker",
            "ms-vscode-remote.remote-containers",
            "ms-vscode.vscode-typescript-tslint-plugin",
            "msjsdiag.debugger-for-chrome",
            "oderwat.indent-rainbow",
            "ritwickdey.live-sass",
            "ritwickdey.live-server",
            "sleistner.vscode-fileutils",
            "streetsidesoftware.code-spell-checker",
            "wix.vscode-import-cost"
        ],
        "postCreateCommand": "yarn install",
        "postStartCommand": "yarn start"
    }
    ```
  - Configuración de Dockerfile
      ```
      Por motivos formativos vamos a generear un Dockerfile para cada parte del proyecto, pero en un proyecto real se debería usar un único Dockerfile para todo el proyecto.
       ```

    ```Dockerfile
    # Use the official Node.js 14 image as a base
    FROM node:14-bullseye

    # Set the working directory
    WORKDIR /usr/src/app

    # Copy package.json and package-lock.json
    COPY package*.json ./

    # Install dependencies
    RUN npm install

    # Copy the rest of the application code
    COPY . .

    # Expose the application port
    EXPOSE 3000

    # Start the application
    CMD ["npm", "start"]
    ```



4. **Personalización del Entorno**
  - Instalación de dependencias


    Para instalar las dependencias del proyecto, podemos ejecutar el siguiente comando en la terminal del DevContainer.
    Eso lo que hace es ejecutar el comando que hemos indicado en el archivo `devcontainer.json` en la propiedad `postCreateCommand`:
    ```
    "postCreateCommand": "yarn install",
    ```
  - Configuración de herramientas y extensiones


  - Variables de entorno

5. **Pruebas y Debugging**
  - Ejecución de pruebas
  - Debugging dentro del DevContainer

6. **Buenas Prácticas**
  - Organización del código
  - Mantenimiento del DevContainer

7. **Recursos Adicionales**
  - Documentación oficial
  
  - Tutoriales y guías

8. **Preguntas y Respuestas**
