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
[Texto del enlace](http://localhost:9000)

### Paso 1: Loggearse con usuario admin y pass admin
![Texto alternativo](/images/2.png)

