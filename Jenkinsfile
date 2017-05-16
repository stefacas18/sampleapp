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
    stage('Analysis Static Code') {
      steps {
        sh 'mvn -DskipTest checkstyle:checkstyle pmd:pmd findbugs:findbugs'
        checkstyle(pattern: 'target/checkstyle-result.xml')
        pmd(pattern: 'target/pmd.xml')
        findbugs(pattern: 'target/findbugsXml.xml')
      }
    }
  }
}