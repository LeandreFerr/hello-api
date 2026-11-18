pipeline {
    agent any

    stages {
        stage('Maven build') {
            agent {
                docker {
                    image 'maven:3.9-eclipse-temurin-21'
                    args '-v $HOME/.m2:/root/.m2:z -u root'
                    reuseNode true
                }
            }

            steps {
                sh 'mvn -v'
                sh 'mvn clean package'
            }
        }

        stage('Docker deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Check deployment') {
            steps {
                sh 'docker compose ps'
            }
        }
    }
}