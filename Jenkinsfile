pipeline {
  agent any
  stages {
    stage('Saludo') {
      steps {
        parallel(
          "Saludo": {
            echo 'Hello World DevOps!'
            
          },
          "Obtener cambios SCM": {
            git 'https://github.com/stefacas18/sampleapp.git'
            
          }
        )
      }
    }
    stage('Pruebas Unitarias') {
      steps {
        sh 'mvn clean test'
        junit 'target/surefire-reports/*.xml'
      }
    }
    stage('Pruebas de Integracion') {
      steps {
        sh 'mvn clean verify -DskipUts'
        junit '/target/failsafe-reports/*.xml'
      }
    }
  }
}