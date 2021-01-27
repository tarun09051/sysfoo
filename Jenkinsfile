pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'Compiling sysfoo App'
        sh 'mvn compile'
        sleep 4
      }
    }

    stage('test') {
      steps {
        echo 'Unit Testing app'
        sh 'mvn clean test'
        sleep 9
      }
    }

    stage('package') {
      steps {
        echo 'Packaging App'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}