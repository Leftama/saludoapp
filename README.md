# 🧙‍♂️ SaludoApp

Una aplicación Java simple que genera saludos personalizados, con pipeline de CI/CD automatizado mediante Jenkins y Maven.

![Java](https://img.shields.io/badge/Java-17+-orange?style=flat-square&logo=java)
![Maven](https://img.shields.io/badge/Maven-3.x-blue?style=flat-square&logo=apache-maven)
![Jenkins](https://img.shields.io/badge/Jenkins-Pipeline-red?style=flat-square&logo=jenkins)

---

## 📘 Tabla de Contenidos

- [Descripción](#-descripción)
- [Características](#-características)
- [Tecnologías](#-tecnologías)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación y Uso](#-instalación-y-uso)
- [Pipeline CI/CD](#-pipeline-cicd)
- [Configuración de Jenkins](#️-configuración-de-jenkins)
- [Beneficios Concretos](#-beneficios-concretos-de-la-automatización)
- [Aspectos Críticos en Equipos Grandes](#-aspectos-críticos-en-equipos-grandes)
- [Aseguramiento de Calidad Pre-Despliegue](#️-aseguramiento-de-calidad-pre-despliegue)
- [Mejoras para Preparar el Pipeline para Producción](#-mejoras-para-preparar-el-pipeline-para-producción)
- [Aprendizajes Clave](#-aprendizajes-clave)
- [Aspectos Más Sorprendentes](#-aspectos-más-sorprendentes)
- [Contribución](#-contribución)
- [Contacto](#-contacto)

---

## 📌 Descripción

**SaludoApp** es una aplicación de consola desarrollada en Java que genera saludos personalizados. Dado un nombre como entrada, la aplicación responde con:

```
¡Hola, <nombre>!
```

Este proyecto está diseñado para demostrar las mejores prácticas de desarrollo con un pipeline completo de CI/CD utilizando Jenkins, Maven y pruebas unitarias automatizadas.

---

## ✨ Características

- 🎯 **Aplicación simple y funcional** - Genera saludos personalizados
- 🔄 **Pipeline CI/CD automatizado** - Integración continua con Jenkins
- ✅ **Pruebas unitarias** - Cobertura de código con JUnit
- 📦 **Gestión de dependencias** - Maven para build y empaquetado
- 🚀 **Despliegue automatizado** - Listo para entornos de producción

---

## 🛠 Tecnologías

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| **Java** | 17+ | Lenguaje de programación principal |
| **Maven** | 3.x | Gestión de dependencias y build |
| **Jenkins** | Estable | Automatización CI/CD |
| **JUnit** | 4+ | Framework de pruebas unitarias |
| **Git** | - | Control de versiones |

---

## 📂 Estructura del Proyecto

```
saludoapp/
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/equipo/saludo/
│   │           └── App.java              # Clase principal
│   └── test/
│       └── java/
│           └── com/equipo/saludo/
│               └── AppTest.java          # Pruebas unitarias
├── Jenkinsfile                           # Pipeline de Jenkins
├── pom.xml                              # Configuración de Maven
└── README.md                            # Documentación del proyecto
```

---

## 📋 Requisitos Previos

Asegúrate de tener instalados los siguientes componentes:

- ☕ **Java JDK 17+**
- 📦 **Maven 3.x**
- 🔧 **Jenkins** (con acceso HTTP)
- 🐙 **Git** y cuenta de **GitHub**

### Verificar instalaciones

```bash
java --version
mvn --version
git --version
```

---

## 🚀 Instalación y Uso

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu_usuario/saludoapp.git
cd saludoapp
```

### 2. Compilar y empaquetar

```bash
mvn clean package
```

### 3. Ejecutar la aplicación

```bash
java -cp target/saludoapp-1.0-SNAPSHOT.jar com.equipo.saludo.App
```

**Salida esperada:**
```
¡Hola, <nombre>!
```

### 4. Ejecutar pruebas

```bash
mvn clean test
```

---

## 🔄 Pipeline CI/CD

El proyecto incluye un `Jenkinsfile` que define un pipeline automatizado con las siguientes etapas:

```groovy
pipeline {
    agent any
    
    tools {
        maven 'Maven 3.9.10'
        jdk 'JDK17'
    }
    
    stages {
        stage('📥 Clonar') {
            steps {
                checkout scm
            }
        }
        
        stage('🔨 Compilar') {
            steps {
                sh 'mvn clean compile'
            }
        }
        
        stage('🧪 Probar') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('📦 Empaquetar') {
            steps {
                sh 'mvn package'
            }
        }
    }
    
    post {
        success { 
            echo '✅ Build exitoso - ¡Aplicación lista para desplegar!' 
        }
        failure { 
            echo '❌ Build falló - Revisa los logs para más detalles' 
        }
    }
}
```

---

## ⚙️ Configuración de Jenkins

### Paso 1: Instalar Jenkins

Sigue la [documentación oficial de Jenkins](https://www.jenkins.io/doc/book/installing/) para tu sistema operativo.

### Paso 2: Configurar herramientas globales

1. Ve a **Manage Jenkins** → **Global Tool Configuration**
2. Configura las siguientes herramientas:
   - **JDK**: JDK17 (instalación automática o manual)
   - **Maven**: Maven 3.9.10

### Paso 3: Crear el pipeline

1. **Nuevo Job** → **Pipeline**
2. **Nombre**: `SaludoApp-CI`
3. **Pipeline**:
   - **Definición**: Pipeline script from SCM
   - **SCM**: Git
   - **Repository URL**: `https://github.com/tu_usuario/saludoapp.git`
   - **Script Path**: `Jenkinsfile`

### Paso 4: Ejecutar el pipeline

Haz clic en **Build Now** y observa cada etapa del pipeline en tiempo real.

---

## ✅ Beneficios Concretos de la Automatización

### Consistencia y Repetibilidad
Cada pipeline ejecuta el flujo de *clonar → compilar → testear → empaquetar* de forma idéntica, reduciendo errores humanos y diferencias entre ambientes.

### Feedback Inmediato
Detecta fallos justo después del `commit`, lo que permite corregir errores de manera temprana.

### Ahorro de Tiempo y Eficiencia
Jenkins se encarga de tareas manuales recurrentes, liberando al equipo para centrarse en desarrollo.

### Trazabilidad y Visibilidad
Guarda historial de builds, logs y artefactos, facilitando auditorías y rastreo de cambios.

## 🧩 Aspectos Críticos en Equipos Grandes

### Ejecución de Pruebas Automatizadas
Fundamental para detectar errores y proteger la calidad cuando hay múltiples desarrolladores.

### Análisis Estático y Métricas de Calidad
Permiten evitar deuda técnica mediante escaneo de código, cobertura y detección temprana de problemas.

### Escalabilidad del Pipeline
En entornos complejos con múltiples servicios o microservicios, es clave distribuir carga y ejecutar tareas en paralelo.

## 🛡️ Aseguramiento de Calidad Pre-Despliegue

### Gatekeeper Automático
Si compilar o testear falla, el pipeline se detiene y notifica al equipo.

### Código como Calidad
Integrar análisis estático, cobertura y escaneo de dependencias fortalece el control antes del despliegue.

### Artefactos Reproducibles
Los builds exitosos garantizan paquetes válidos y listos para entornos posteriores (staging o producción).

## 🔧 Mejoras para Preparar el Pipeline para Producción

1. **Agregar análisis estático y de seguridad** (`mvn verify sonar:sonar` + SAST/DAST)
2. **Construcción de imágenes Docker** y despliegue a registries
3. **Paralelización de pruebas** para optimizar velocidad y recursos
4. **Pipeline multietapa de despliegue** (staging → producción, con control manual o por tag)
5. **Notificaciones automáticas**: Slack, correo o dashboards con cobertura y resultados
6. **Gestión segura de credenciales** mediante Jenkins Credentials, evitando exponer secretos
7. **Monitoreo del pipeline**: métricas como tiempo de build, tasa de éxito, cobertura, alertas

## 🎓 Aprendizajes Clave

- La importancia de un **pipeline como código**, versionado junto al proyecto
- Que un proceso reproducible y centralizado mejora la colaboración y calidad del equipo
- El valor de automatizar **todo el flujo de CI**: build, prueba, empaquetado y despliegue

## 😲 Aspectos Más Sorprendentes

- Que *"en lugar de esperar a que todo esté listo, Jenkins entrega feedback inmediato con cada commit"*, mejorando la agilidad y reduciendo errores
- Lo **rápido y claro** que se detectan errores
- La **escala y flexibilidad** que permite integrar análisis, seguridad, Docker y despliegues en un solo pipeline

---

## 🤝 Contribución

¡Las contribuciones son bienvenidas! Si quieres mejorar este proyecto:

1. **Fork** el repositorio
2. **Crea** una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. **Commit** tus cambios (`git commit -m 'Agregar nueva funcionalidad'`)
4. **Push** a la rama (`git push origin feature/nueva-funcionalidad`)
5. **Abre** un Pull Request

---

## 📞 Contacto

- 📧 **Email**: caraya.salazar@gmail.com
- 🐙 **GitHub**: [@Leftama](https://github.com/Leftama)
- 💼 **LinkedIn**: [Tu Perfil](https://www.linkedin.com/in/carayasalazar/)

---

<div align="center">
  <strong>⭐ Si este proyecto te fue útil, no olvides darle una estrella ⭐</strong>
</div>