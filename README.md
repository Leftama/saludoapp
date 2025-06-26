# 🧙‍♂️ SaludoApp

Aplicación Java simple que genera saludos personalizados, con pipeline de CI/CD automatizado mediante Jenkins y Maven.

---

## 📘 Tabla de Contenidos

1. [Descripción](#descripción)  
2. [Tecnologías](#tecnologías)  
3. [Estructura del proyecto](#estructura-del-proyecto)  
4. [Requisitos](#requisitos)  
5. [Instalación y ejecución local](#instalación-y-ejecución-local)  
6. [Pipeline CI con Jenkins](#pipeline-ci-con-jenkins)  
7. [Configuración de Jenkins](#configuración-de-jenkins)  
8. [Beneficios & buenas prácticas](#beneficios--buenas-prácticas)  
9. [Mejoras para producción](#mejoras-para-producción)  

---

## 📌 Descripción

**SaludoApp** es una aplicación de consola en Java que, dado un nombre, imprime:  
¡Hola, <nombre>!
Ideal para demostrar un pipeline básico de CI/CD usando Jenkins, Maven y pruebas unitarias.

---

## 🧩 Tecnologías

- Java 17+  
- Maven 3.x  
- Jenkins (versión estable)  
- Git + GitHub  
- JUnit 4+ (para pruebas unitarias)

---

## 📂 Estructura del proyecto

saludoapp/
├── src/
│ ├── main/java/com/equipo/saludo/App.java
│ └── test/java/com/equipo/saludo/AppTest.java
├── Jenkinsfile
└── pom.xml

---

## ✅ Requisitos

- **Java JDK 17+**  
- **Maven 3.x**  
- **Jenkins** (con acceso HTTP)  
- Cuenta de **GitHub**, con token si el repositorio es privado

---

## 🔧 Instalación y ejecución local

```bash
git clone https://github.com/tu_usuario/saludoapp.git
cd saludoapp
mvn clean package
java -cp target/saludoapp-1.0-SNAPSHOT.jar com.equipo.saludo.App
Deberías ver en consola: ¡Hola, <nombre>!
```
## 🧪 Pruebas unitarias
El archivo AppTest.java contiene una prueba simple de JUnit.
Ejecuta:
```bash
mvn clean test
```
## 🚀 Pipeline CI con Jenkins
Archivo Jenkinsfile:

```bash
pipeline {
  agent any
  tools {
    maven 'Maven 3.9.10'
    jdk 'JDK17'
  }
  stages {
    stage('Clonar') {
      steps {
        git 'https://github.com/tu_usuario/saludoapp.git'
      }
    }
    stage('Compilar') {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('Probar') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Empaquetar') {
      steps {
        sh 'mvn package'
      }
    }
  }
  post {
    success { echo '✅ Build exitoso' }
    failure { echo '❌ Build falló' }
  }
}
```
## ⚙️ Configuración de Jenkins

Instala Jenkins (ver [documentación oficial]).
Desde Manage Jenkins → Global Tool Configuration, registra:
- JDK17 (instalado o automático)
- Maven 3.9.10
- Crea un Job tipo Pipeline:
- Nombre: SaludoApp-CI
- Definición: Pipeline script from SCM
- SCM: Git
- - URL: https://github.com/tu_usuario/saludoapp.git
- Ruta del script: Jenkinsfile
- Haz clic en Build Now y verifica cada etapa.

## 🌟 Beneficios & buenas prácticas
- Pipeline escalable y confiable: sigue el flujo de clonar → compilar → testear → empaquetar
- Feedback rápido en caso de errores o regresiones
- Historial de builds con logs y reportes
- Integración sencilla con herramientas de análisis y despliegue

## 🏆 Mejoras para entornos productivos
- Añadir análisis estático: mvn verify sonar:sonar + SonarQube
- Construcción y push de imagen Docker
- Pipeline paralelo para pruebas unitarias e integración
- Despliegue automático a staging/producción con Helm, Kubernetes o scripts
- Notificaciones a Slack o correo
- Uso de Jenkins Credentials para gestion de secrets
