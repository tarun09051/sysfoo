pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Compiling sysfoo App'
        sh 'mvn compile'
        sleep 4
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Unit Testing app'
        sh 'mvn clean test'
        sleep 9
      }
    }

    stage('package') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Packaging App'
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.war'
      }
    }

    stage('Docker B&P') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {

            def dockerImage = docker.build("tarunvashisth/sysfoo:v${env.BUILD_ID}", "./")

            dockerImage.push()

            dockerImage.push("latest")
            dockerImage.push("dev")

          }
        }

      }
    }
    
    stage('Deploy to Dev') {

      when {
        beforeAgent true
        branch 'master'
      }

      agent any

      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}
