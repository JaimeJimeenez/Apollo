# Apollo

Este repositorio contiene el código fuente e infraestructura para un framework de chatbot basado en microservicios. Está diseñado para ser modular y adaptable a distintos proyectos, permitiendo integrarlo con cualquier frontend (por ejemplo, Angular, React, etc.) a través de una API robusta. El entorno se gestiona mediante contenedores Docker y se orquesta con Docker Compose, contando además con integración continua mediante GitHub Actions.

## Tabla de Contenidos
- [Visión General](#visión-general)
- [Arquitectura](#arquitectura)
- [Características](#características)
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Integración Continua y Workflows](#integración-continua-y-workflows)
- [Roadmap de Desarrollo](#roadmap-de-desarrollo)
- [Contribución](#contribución)
- [Licencia](#licencia)

## Visión General

El framework de chatbot se compone de múltiples microservicios independientes que gestionan aspectos clave de la interacción conversacional:

- **API Gateway:** Punto de entrada central (implementado en FastAPI) que enruta las solicitudes a los servicios correspondientes.
- **Servicio NLP:** Procesa y analiza las entradas de lenguaje natural.
- **Servicio de Gestión de Diálogos:** Maneja el flujo de la conversación y el contexto.
- **Servicio de Integración Externa (Opcional):** Se conecta con APIs de terceros para enriquecer las respuestas.
- **Servicio de Autenticación (Opcional):** Gestiona la autenticación y autorización de usuarios.

Además, se incluye un frontend de referencia desarrollado en Angular, que sirve para demostrar cómo consumir la API del Gateway.

## Arquitectura

El sistema se estructura en contenedores Docker que se orquestan mediante Docker Compose. La comunicación se realiza a través de una API centralizada en el Gateway que dirige las solicitudes a los distintos microservicios (NLP, Diálogo, etc.). También se incluye una base de datos PostgreSQL para almacenar información relevante.

![Diagrama de Arquitectura](./docs/arquitectura.png)  
*Nota: Agrega un diagrama de arquitectura si lo tienes disponible.*

## Características

- **Microservicios Desacoplados:** Cada servicio se ejecuta en su propio contenedor.
- **API Unificada:** El Gateway centraliza la comunicación y enruta las solicitudes.
- **Contenedorización y Orquestación:** Uso de Docker y Docker Compose para un entorno de desarrollo consistente.
- **Integración Continua:** Workflows configurados en GitHub Actions para ejecutar tests y validaciones.
- **Frontend de Referencia:** Aplicación Angular para interactuar con el backend, adaptable a otros frameworks.

## Requisitos Previos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Git](https://git-scm.com/)
- (Opcional) [Node.js y Angular CLI](https://angular.io/cli) para desarrollo y personalización del frontend

## Instalación

1. **Clonar el Repositorio**
   ```bash
   git clone https://github.com/tuusuario/chatbot-framework.git
   cd chatbot-framework

2. **Configurar el Entorno**
- Asegúrate de tener Docker y Docker Compose instalados en tu máquina.
3. **Construir y Levantar los Contenedores**
    ```bash
    docker-compose up --build --no-cache
4. **Acceder a la Aplicación**
- **Frontend Angular**:[http://localhost:4200]
- **API Gateway**: [http://localhost:0000]
- Otros servicios estarán disponibles en los puertos definidos en docker-compose.yml
## Uso
- **Frontend**: La aplicación Angular se comunica con el API Gateway usando la variable de entorno API_URL
- **API Gateway**: Enruta solicitudes a los servicios de NLP y Gestión de Diálogos. Dispone de un endpoint /ping para comprobar su estado.
- **Servicios Backend**:
    - El **Servicio NLP** procesa entradas y retorna respuestas (inicialmente estáticas o predefinidas).
    - El **Servicio de Diálogo** gestiona flujos conversacionales básicos.
Consulta la documentación de la API (por ejemplo, con Swagger si se ha integrado) para más detalles sobre los endpoints y formatos de respuesta.
## Estructura del Proyecto

    apollo/
    ├── docker-compose.yaml        
    ├── README.md                  
    ├── frontend/           
    ├── gateway/            
    ├── nlp/                
    ├── dialog/             
    ├── integration/        
    └── auth/               

## Integración Continua y Workflows
- **GitHub Actions**:

    Los workflows se encuentran en .github/workflows/ci.yml.
    - Se ejecutan tests unitarios y de integración en cada push y pull request.
    - Se realizan validaciones de linting y se notifican errores críticos.

Consulta el archivo de configuración para entender el proceso de integración continua.