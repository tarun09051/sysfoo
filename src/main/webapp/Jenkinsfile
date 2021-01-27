pipeline{

    agent any

    tools{
        maven 'Maven 3.6.3'
    }   

    stages{
        stage('build'){
            steps{
                echo 'Compiling sysfoo App'
                sh 'mvn compile'
                sleep 4
            }
        }
        stage('test'){
            steps{
                echo 'Unit Testing app'
                sh 'mvn clean test'
                sleep 9
            }
        }
        stage('package'){
            steps{
                echo 'Packaging App'
                sh 'mvn package -DskipTests'
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
            }
        }
    }
    
}

