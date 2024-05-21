# Análisis de Código con SonarQube en Linux

Este proyecto proporciona una guía para configurar y ejecutar análisis de código utilizando SonarQube en un entorno Linux. SonarQube es una plataforma para el análisis continuo de calidad de código, que detecta bugs, vulnerabilidades y problemas de calidad en tu código fuente.

## Requisitos

Antes de comenzar, asegúrate de tener instalados los siguientes componentes en tu sistema:
- [Docker](https://www.docker.com/)
- [SonarScanner](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)

## Instalación

### Paso 1: Docker compose con el siguiente código

```bash
version: '2'

services:
  sonarqube:
    image: sonarqube
    ports:
      - "9000:9000"
    networks:
      - sonarnet
    environment:
      - SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar
      - SONARQUBE_JDBC_USERNAME=sonar
      - SONARQUBE_JDBC_PASSWORD=sonar
    volumes:
      - sonarqube_conf:/opt/sonarqube/conf
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_bundled-plugins:/opt/sonarqube/lib/bundled-plugins

  db:
    image: postgres
    networks:
      - sonarnet
    environment:
      - POSTGRES_USER=sonar
      - POSTGRES_PASSWORD=sonar
    volumes:
      - postgresql:/var/lib/postgresql
      - postgresql_data:/var/lib/postgresql/data

networks:
  sonarnet:
    driver: bridge

volumes:
  sonarqube_conf:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_bundled-plugins:
  postgresql:
  postgresql_data:

```
### Paso 2: Ejecutar docker-compose.yml
```bash
    sudo docker-compose up -d
```
![Texto alternativo](/images/1.png)

### Paso 3: Verificar con docker ps
![Texto alternativo](/images/9.png)

## Acceder a SonarQube

Abre tu navegador y accede a:
[http://localhost:9000](http://localhost:9000)

### Paso 1: Loggearse en SonarQube
Ingrese con usuario admin y contraseña admin

### Paso 2: Cree un proyecto local

![Texto alternativo](/images/3.png)

### Paso 3: Configure y cree el proyecto
![Texto alternativo](/images/4.png)

### Paso 4: Genere el token
![Texto alternativo](/images/5.png)

### Paso 5: Configure de acuerdo a las caracteristicas de su proyecto y máquina
![Texto alternativo](/images/6.png)

### Paso 6: Ejecute el scanner en el directorio del proyecto que desea analizar
![Texto alternativo](/images/8.png)

### Paso 7: Revise los reportes y analisis
![Texto alternativo](/images/7.png)

