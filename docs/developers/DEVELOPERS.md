# Levantar servidor para desarrollo

Pre requisitos:
- [Maven](https://maven.apache.org/download.cgi)
- [Git](https://git-scm.com/downloads)
- Java - OpenJDK  (8, 11)
- [Nodejs](https://nodejs.org/en/download/) (>=12.14.1)
- [yarn](https://legacy.yarnpkg.com/en/docs/install) (>=1.21.1)

# Levantar el Backend
Para levantar el backend en modo desarrollo necesitas:

1. Hacer un fork al projecto https://github.com/project-openubl/xml-builder

2. clonar el project que acabas de hacer fork:
```
git clone https://github.com/carlosthe19916/xml-builder.git 
```

recuerda cambiar `carlosthe19916` por el usuario con el que hiciste Fork en el paso anterior

3. Ubicarte en la carpeta que acabas de descargar
```
cd xml-builder
```

3. Descargar dependencias
```
./mvnw install -DskipTests
```

4. Arrancar servidor:

```
./mvnw clean compile quarkus:dev -f api/ -DnoDeps
```

Ó

```
./mvnw clean compile quarkus:dev -f api-signer/ -DnoDeps
```

Eso es todo. Podrás ver el servidor corriendo en http://localhost:8080/


# Levantar el Frontend

1. Hacer un fork al projecto https://github.com/project-openubl/xml-builder-ui o https://github.com/project-openubl/xml-builder-ee-ui

2. clonar el project que acabas de hacer fork:
```
git clone https://github.com/project-openubl/xml-builder-ui.git
```

Ó

```
git clone https://github.com/project-openubl/xml-builder-ee-ui.git
```

recuerda cambiar `carlosthe19916` por el usuario con el que hiciste Fork en el paso anterior.

3. Ubicarte en la carpeta que acabas de descargar
```
cd xml-builder-ui
```

Ó

```
cd xml-builder-ee-ui
```

4. Instalar las dependencias

```
yarn install
```

5. Iniciar el servidor
```
yarn start
```

Abrir el navegador y dirigirte a http://localhost:3000/
