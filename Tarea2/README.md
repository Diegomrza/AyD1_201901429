# Dockerizar una Aplicación Vue.js con Vite

Este documento describe los pasos necesarios para dockerizar una aplicación hecha en Vue.js creada con Vite para ejecutarla localmente en el puerto 80.

## Prerrequisitos

1. Tener Docker instalado en tu sistema.
2. Contar con una aplicación Vue.js creada con Vite.

## Pasos

### 1. Crear el archivo `Dockerfile`

En la raíz del proyecto, crear un archivo llamado `Dockerfile` con el siguiente contenido:

```dockerfile
# Etapa 1: Construcción
FROM node:18 AS build
WORKDIR /app
COPY package*.json ./ 
RUN npm install
COPY . . 
RUN npm run build

# Etapa 2: Servidor
FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### 2. Crear el archivo `.dockerignore`

Crea un archivo `.dockerignore` para excluir archivos innecesarios del contexto de construcción:

```
node_modules
dist
```

### 3. Construir la imagen de Docker

Ejecuta el siguiente comando en la terminal para construir la imagen de Docker:

```bash
docker build -t vuejs-vite-app .
```

### 4. Ejecutar el contenedor

Inicia un contenedor basado en la imagen creada:

```bash
docker run -d -p 80:80 --name vuejs-vite-container vuejs-vite-app
```

### 5. Acceder a la aplicación

Abre tu navegador y accede a `http://localhost` para ver tu aplicación en ejecución.

## Notas

- Este despliegue está configurado únicamente para uso local.
- Asegúrate de que tu aplicación esté correctamente configurada antes de construir la imagen.

¡Listo! Tu aplicación Vue.js con Vite ahora está dockerizada y lista para ejecutarse localmente.